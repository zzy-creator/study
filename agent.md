[https://ata.atatech.org/articles/11020600930?spm=ata.21736010.0.0.7e157536CiN1h7#M2RhMjc4](https://ata.atatech.org/articles/11020600930?spm=ata.21736010.0.0.7e157536CiN1h7#M2RhMjc4) 该文章学习摘要👇

### agent loop
对话agent时，agent生成回复&执行操作的loop代码（也就是agent代码的主框架）：

```javascript
const messages: MessageParam[] = [{ role: "user", content: userInput }];

while (true) {
  const response = await client.messages.create({
    model: "claude-opus-4-6",
    max_tokens: 8096,
    tools: toolDefinitions,
    messages,
  });

  if (response.stop_reason === "tool_use") {
    const toolResults = await Promise.all(
      response.content
        .filter((b) => b.type === "tool_use")
        .map(async (b) => ({
          type: "tool_result" as const,
          tool_use_id: b.id,
          content: await executeTool(b.name, b.input),
        }))
    );
    messages.push({ role: "assistant", content: response.content });
    messages.push({ role: "user", content: toolResults });
  } else {
    return response.content.find((b) => b.type === "text")?.text ?? "";
  }
}
```

就是每次循环，用当前的上下文调用llm，然后判断要不要用工具，如果不需要工具就结束；否则调用工具然后把内容加到上下文，继续循环

### Harness
[https://zhuanlan.zhihu.com/p/2014014859164026634](https://zhuanlan.zhihu.com/p/2014014859164026634)

**<font style="color:rgb(25, 27, 31);">Harness Engineering</font>**<font style="color:rgb(25, 27, 31);">是指围绕 AI Agent（特别是 Coding Agent）设计和构建</font>**<font style="color:rgb(25, 27, 31);">约束机制、反馈回路、工作流控制和持续改进循环</font>**<font style="color:rgb(25, 27, 31);">的系统工程实践。它解决的核心问题是：当 AI Agent 拥有了强大的代码生成能力后，如何确保其输出的可靠性、一致性和长期可维护性。</font>

<font style="color:rgb(25, 27, 31);"></font>

#### <font style="color:rgb(25, 27, 31);">why need？</font>
+ <font style="color:rgb(25, 27, 31);">OpenAI 团队说得很直接：</font>**<font style="color:rgb(25, 27, 31);">真正卡你的不是 Agent 写代码的能力，而是围绕它的结构、工具和反馈机制跟不上</font>**<font style="color:rgb(25, 27, 31);">. 五个独立团队得出了相同结论：基础设施才是瓶颈，而非智能水平。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2026/png/88656377/1774604417572-133aa916-3f40-40cb-a753-f61a66081e7e.png" width="1080" title="" crop="0,0,1,1" id="u682c1143" class="ne-image">

一、上下文架构：**<font style="color:rgb(25, 27, 31);">分层上下文与渐进式披露</font>**<font style="color:rgb(25, 27, 31);">：</font>

| <font style="color:rgb(25, 27, 31);">层级</font> | <font style="color:rgb(25, 27, 31);">加载时机</font> | <font style="color:rgb(25, 27, 31);">内容示例</font> | <font style="color:rgb(25, 27, 31);">上下文占用</font> |
| :--- | :--- | :--- | :--- |
| <font style="color:rgb(25, 27, 31);">Tier 1：会话常驻</font> | <font style="color:rgb(25, 27, 31);">每次会话自动加载</font> | <font style="color:rgb(25, 27, 31);">AGENTS.md / CLAUDE.md，项目结构概览</font> | <font style="color:rgb(25, 27, 31);">最小</font> |
| <font style="color:rgb(25, 27, 31);">Tier 2：按需加载</font> | <font style="color:rgb(25, 27, 31);">特定子 Agent 或技能被调用时</font> | <font style="color:rgb(25, 27, 31);">专业化 Agent 的上下文、领域知识（skills）</font> | <font style="color:rgb(25, 27, 31);">中等</font> |
| <font style="color:rgb(25, 27, 31);">Tier 3：持久化知识库</font> | <font style="color:rgb(25, 27, 31);">Agent 主动查询时</font> | <font style="color:rgb(25, 27, 31);">研究文档、规格说明、历史会话</font> | <font style="color:rgb(25, 27, 31);">按需</font> |


<font style="color:rgba(25, 26, 31, 0.9);">写 AGENTS.md 这件事，本质上是在回答一个问题：</font>**<font style="color:rgba(25, 26, 31, 0.9);">如果一个新来的（AI）同事要在你的项目里干活，你最想叮嘱它什么？</font>**

+ **<font style="color:rgba(25, 26, 31, 0.9);">多写"不要做什么"</font>**
+ **<font style="color:rgba(25, 26, 31, 0.9);">写能直接使用的命令，如 npm run dev</font>**
+ **<font style="color:rgba(25, 26, 31, 0.9);">先写起来，逐步迭代</font>**

**<font style="color:rgba(25, 26, 31, 0.9);"></font>**

二、Agent专业化

**<font style="color:rgb(25, 27, 31);">核心原则</font>**<font style="color:rgb(25, 27, 31);">：专注于特定领域、拥有受限工具的 Agent 优于拥有全部权限的通用 Agent。</font>

**<font style="color:rgb(25, 27, 31);">实践中的角色分工</font>**<font style="color:rgb(25, 27, 31);">：</font>

| <font style="color:rgb(25, 27, 31);">Agent 角色</font> | <font style="color:rgb(25, 27, 31);">职责范围</font> | <font style="color:rgb(25, 27, 31);">工具权限</font> |
| :--- | :--- | :--- |
| <font style="color:rgb(25, 27, 31);">研究 Agent</font> | <font style="color:rgb(25, 27, 31);">探索代码库、分析实现细节</font> | <font style="color:rgb(25, 27, 31);">只读（Read, Grep, Glob）</font> |
| <font style="color:rgb(25, 27, 31);">规划 Agent</font> | <font style="color:rgb(25, 27, 31);">将需求分解为结构化任务</font> | <font style="color:rgb(25, 27, 31);">只读，无写入权限</font> |
| <font style="color:rgb(25, 27, 31);">执行 Agent</font> | <font style="color:rgb(25, 27, 31);">实现单个具体任务</font> | <font style="color:rgb(25, 27, 31);">限定范围的读写权限</font> |
| <font style="color:rgb(25, 27, 31);">审查 Agent</font> | <font style="color:rgb(25, 27, 31);">审计完成的工作，标记问题</font> | <font style="color:rgb(25, 27, 31);">只读 + 标记权限</font> |
| <font style="color:rgb(25, 27, 31);">调试 Agent</font> | <font style="color:rgb(25, 27, 31);">修复审查发现的问题</font> | <font style="color:rgb(25, 27, 31);">限定范围的修复权限</font> |
| <font style="color:rgb(25, 27, 31);">清理 Agent</font> | <font style="color:rgb(25, 27, 31);">对抗熵积累，清理低质量代码</font> | <font style="color:rgb(25, 27, 31);">读写权限</font> |


<font style="color:rgb(25, 27, 31);">  
</font><font style="color:rgb(25, 27, 31);"> 三、持久化记忆</font>

**<font style="color:rgb(25, 27, 31);">核心原则</font>**<font style="color:rgb(25, 27, 31);">：进度持久化在文件系统上，而非上下文窗口中。每次新 Agent 会话从零开始，通过文件系统制品重建上下文。</font>

<font style="color:rgb(25, 27, 31);">Anthropic 解决这一问题的方案堪称经典：</font>

**<font style="color:rgb(25, 27, 31);">初始化 Agent</font>**<font style="color:rgb(25, 27, 31);">：首次会话使用专门的 prompt，要求模型建立初始环境——init.sh 脚本、claude-progress.txt 进度文件和初始 git 提交。</font>

**<font style="color:rgb(25, 27, 31);">编码 Agent</font>**<font style="color:rgb(25, 27, 31);">：后续每次会话要求模型在做出增量进展的同时，留下结构化更新。</font>

<font style="color:rgb(25, 27, 31);">每个编码 Agent 的典型会话启动流程如下：</font>

<font style="color:rgb(25, 27, 31);">1. 运行 pwd 查看工作目录</font>

<font style="color:rgb(25, 27, 31);">2. 读取 git log 和进度文件，了解最近的工作</font>

<font style="color:rgb(25, 27, 31);">3. 读取 feature list 文件，选择最高优先级的未完成功能</font>

<font style="color:rgb(25, 27, 31);">4. 启动开发服务器，运行基础端到端测试</font>

<font style="color:rgb(25, 27, 31);">5. 确认基本功能正常后，开始新功能开发</font>

<font style="color:rgb(25, 27, 31);">关键发现：</font>**<font style="color:rgb(25, 27, 31);">使用 JSON 格式追踪 feature 状态比 Markdown 更有效</font>**<font style="color:rgb(25, 27, 31);">，因为 Agent 不太可能不恰当地修改或覆盖结构化数据。</font>



四、结构化执行

**<font style="color:rgb(25, 27, 31);">核心原则</font>**<font style="color:rgb(25, 27, 31);">：将思考与执行分离。研究和规划在受控阶段进行，执行基于验证过的计划，验证通过自动化反馈（测试、Linter、CI）和人类审查完成。</font>

<font style="color:rgb(25, 27, 31);">所有团队都施加了刻意的执行序列：</font>**<font style="color:rgb(25, 27, 31);">理解 → 规划 → 执行 → 验证</font>**<font style="color:rgb(25, 27, 31);">。</font>

**<font style="color:rgb(25, 27, 31);">人工检查点的价值</font>**<font style="color:rgb(25, 27, 31);">：审查计划远比审查代码快。当规格正确时，实现自然可靠。当规格有误时，可以在 500 行代码生成之前及时纠正。</font>

<font style="color:rgb(25, 27, 31);">  
</font><img src="https://intranetproxy.alipay.com/skylark/lark/0/2026/png/88656377/1774605467800-1e2b7bb7-85fb-4724-8f04-72c401e4ee91.png" width="1080" title="" crop="0,0,1,1" id="u5dd03e7e" class="ne-image">

#### 实践-各层文件详细讲解
[https://tw93.fun/2026-03-12/claude.html](https://tw93.fun/2026-03-12/claude.html)

#### 一些实战的经验
+ **<font style="color:rgb(25, 27, 31);">设计环境，而非编写代码。</font>**<font style="color:rgb(25, 27, 31);">工程师的工作转向为 Agent 准备高效运行的环境。当 Agent 卡住时，不是"更加努力"，而是诊断"缺少什么能力"并让 Agent 自己构建该能力。</font>
+ **<font style="color:rgb(25, 27, 31);">械化地执行架构约束。</font>**<font style="color:rgb(25, 27, 31);">他们为每个领域定义了依赖方向——Types → Config → Repo → Service → Runtime → UI——并用自定义 Linter 和结构测试自动检测违规。文档中记录是不够的；如果不能机械化地强制执行，Agent 就会偏离。</font>
+ **<font style="color:rgb(25, 27, 31);">将可观测性连接到 Agent。</font>**<font style="color:rgb(25, 27, 31);">他们将 Chrome DevTools 连接到运行时，使 Agent 能够捕获 DOM 快照和截图。通过赋予查询日志和指标的能力，"将启动时间降至 800ms 以下"变成了可度量的目标。</font>
+ <img src="https://intranetproxy.alipay.com/skylark/lark/0/2026/png/88656377/1774860127016-e3b31d2c-2b7f-4351-9b51-a83de25d7538.png" width="1080" title="" crop="0,0,1,1" id="u539feebc" class="ne-image">



#### <font style="color:rgb(25, 27, 31);">关键 Harness 组件检查清单</font>
| <font style="color:rgb(25, 27, 31);">组件</font> | <font style="color:rgb(25, 27, 31);">用途</font> | <font style="color:rgb(25, 27, 31);">优先级</font> |
| :--- | :--- | :--- |
| <font style="color:rgb(25, 27, 31);">AGENTS.md / CLAUDE.md</font> | <font style="color:rgb(25, 27, 31);">会话常驻上下文，动态反馈循环</font> | <font style="color:rgb(25, 27, 31);">P0</font> |
| <font style="color:rgb(25, 27, 31);">自定义 Linter + 结构测试</font> | <font style="color:rgb(25, 27, 31);">机械化执行架构约束</font> | <font style="color:rgb(25, 27, 31);">P0</font> |
| <font style="color:rgb(25, 27, 31);">CI/CD 管道</font> | <font style="color:rgb(25, 27, 31);">自动化测试和验证反馈</font> | <font style="color:rgb(25, 27, 31);">P0</font> |
| <font style="color:rgb(25, 27, 31);">进度文件 (progress.txt / JSON)</font> | <font style="color:rgb(25, 27, 31);">跨会话的持久化记忆</font> | <font style="color:rgb(25, 27, 31);">P1</font> |
| <font style="color:rgb(25, 27, 31);">功能列表文件 (feature_list.json)</font> | <font style="color:rgb(25, 27, 31);">结构化完成标准</font> | <font style="color:rgb(25, 27, 31);">P1</font> |
| <font style="color:rgb(25, 27, 31);">浏览器自动化 (Puppeteer MCP)</font> | <font style="color:rgb(25, 27, 31);">端到端测试验证</font> | <font style="color:rgb(25, 27, 31);">P1</font> |
| <font style="color:rgb(25, 27, 31);">可观测性集成</font> | <font style="color:rgb(25, 27, 31);">Agent 可查询日志/指标</font> | <font style="color:rgb(25, 27, 31);">P2</font> |
| <font style="color:rgb(25, 27, 31);">熵管理 Agent</font> | <font style="color:rgb(25, 27, 31);">定期清理低质量代码</font> | <font style="color:rgb(25, 27, 31);">P2</font> |
| <font style="color:rgb(25, 27, 31);">专业化子 Agent</font> | <font style="color:rgb(25, 27, 31);">分工协作减少上下文污染</font> | <font style="color:rgb(25, 27, 31);">P2</font> |
| <font style="color:rgb(25, 27, 31);">MCP 工具集成</font> | <font style="color:rgb(25, 27, 31);">连接外部工具和数据</font> | <font style="color:rgb(25, 27, 31);">P2</font> |


#### <font style="color:rgb(25, 27, 31);">业界共识与分歧全景</font>
<img src="https://intranetproxy.alipay.com/skylark/lark/0/2026/png/88656377/1774927911235-89729944-dcda-45c3-8e3c-70178dc17be7.png" width="1080" title="" crop="0,0,1,1" id="uf008dbdf" class="ne-image">

#### <font style="color:rgb(25, 27, 31);">总结</font>
<font style="color:rgb(25, 27, 31);">Harness Engineering 标志着 AI 辅助开发从"让模型写代码"到"设计让模型可靠工作的系统"的范式转变。这不是等更强模型出来就能解决的事——模型越强，Harness 反而越重要。六大共识已经清晰（基础设施是瓶颈、文档要活、思考与执行分离、上下文不是越多越好、约束必须自动化、工程师角色在转变），但棕地项目改造、功能验证体系、AI 代码的长期可维护性三大空白区仍待填补。如果只记一句话：</font>**<font style="color:rgb(25, 27, 31);">瓶颈不在智能，而在基础设施。</font>**<font style="color:rgb(25, 27, 31);">正如 Addy Osmani 所言："AI 编码的兴起并没有取代软件工程的工艺——它抬高了工艺的门槛。"</font>
