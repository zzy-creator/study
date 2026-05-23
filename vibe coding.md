skills：技能，按需加载；rules：规则，用于约束agent，告诉agent一定要做xxx，一定不能做xxx，每次对话都会读取

### <font style="color:rgb(25, 27, 31);">缺乏架构思维的 Vibe Coding 是在加速产生垃圾代码</font>
<font style="color:rgb(25, 27, 31);">有开发者分享过真实案例：3 小时用 Vibe Coding 构建了一个原型，体验非常流畅。但回过头看代码时，代码一团糟，最终花了 5 个小时重构。</font>

<font style="color:rgb(25, 27, 31);">我把这种现象称为 </font>**<font style="color:rgb(25, 27, 31);">"</font>**[**<font style="color:rgb(9, 64, 142);">熵增</font>**](https://zhida.zhihu.com/search?content_id=269143476&content_type=Article&match_order=1&q=%E7%86%B5%E5%A2%9E&zhida_source=entity)**<font style="color:rgb(25, 27, 31);">"</font>**<font style="color:rgb(25, 27, 31);">：</font>**<font style="color:rgb(25, 27, 31);">没有架构约束的 AI 编程，随着时间推移，代码只会变得越来越混乱，难以维护</font>**<font style="color:rgb(25, 27, 31);">。</font>

<font style="color:rgb(25, 27, 31);">当然，如果只是快速原型是没什么问题，怎么快怎么来，如果要继续迭代，就行不通。</font>

### <font style="color:rgb(25, 27, 31);">AI 够强了，瓶颈可能在于人</font>
<font style="color:rgb(25, 27, 31);">Claude Opus 4.5、</font>[<font style="color:rgb(9, 64, 142);">GPT-5.2</font>](https://zhida.zhihu.com/search?content_id=269143476&content_type=Article&match_order=1&q=GPT-5.2&zhida_source=entity)<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">这些模型的能力已经非常强了，模型的能力还会继续提升，但现在的瓶颈可能是人。</font>

<font style="color:rgb(25, 27, 31);">如果表述不清晰、上下文混乱，AI 就会产生</font>**<font style="color:rgb(25, 27, 31);">幻觉</font>**<font style="color:rgb(25, 27, 31);">，编造 API、引入不存在的库、丢失架构约束。</font>

<font style="color:rgb(25, 27, 31);">这就引出了一个核心公式：</font>**<font style="color:rgb(25, 27, 31);">AI 输出质量 = 模型能力 × 输入质量</font>**<font style="color:rgb(25, 27, 31);">。</font>

<font style="color:rgb(25, 27, 31);">模型能力对所有人都一样。</font>**<font style="color:rgb(25, 27, 31);">真正的变量，是你定义任务、组织上下文的能力。</font>**

<font style="color:rgb(25, 27, 31);">怎么提升输入质量？答案是：</font>**<font style="color:rgb(25, 27, 31);">将想法固化为受控的文件</font>**<font style="color:rgb(25, 27, 31);">，规格文档、架构约束、任务工作流等等。</font>

## <font style="color:rgb(25, 27, 31);">架构思维</font>
### <font style="color:rgb(25, 27, 31);">架构的重要性</font>
<font style="color:rgb(25, 27, 31);">有了好的架构，AI 可以快速迭代功能，同时保持项目的稳定性和可维护性。架构为 AI 划定了边界，让它知道什么该做、什么不该做。</font>

**<font style="color:rgb(25, 27, 31);">架构能力比编码能力更重要</font>**<font style="color:rgb(25, 27, 31);">。以后的模式会发生改变：人类负责架构设计和任务定义，AI 负责代码生成。</font>

### <font style="color:rgb(25, 27, 31);">Vibe Coding 的架构是什么样的</font>
<font style="color:rgb(25, 27, 31);">首先你需要有一套符合规范的规格定义</font>

+ <font style="color:rgb(25, 27, 31);">结构化的需求文档</font>
+ <font style="color:rgb(25, 27, 31);">技术约束</font>
+ <font style="color:rgb(25, 27, 31);">代码结构设计</font>
+ <font style="color:rgb(25, 27, 31);">项目的最佳实践</font>
+ <font style="color:rgb(25, 27, 31);">开发过程的 SOP，包含测试、验收等等</font>

## <font style="color:rgb(25, 27, 31);">工程化</font>
### <font style="color:rgb(25, 27, 31);">1. 文档化：将项目逻辑沉淀为 AI 可读的文档</font>
**<font style="color:rgb(25, 27, 31);">文档不再是事后的附加品，而是驱动开发的核心工件。</font>**

<font style="color:rgb(25, 27, 31);">以 Claude Code 为例，常见的文档结构：</font>

```plain
project-root/
├── .claude/
│   ├── CLAUDE.md              # 整个规则的入口
│   ├── rules/                 # 规则与约束
│   │   ├── code-style.md      # 代码风格规范
│   │   ├── components.md      # 组件设计规范
│   │   ├── api-design.md      # API 设计规范
│   │   └── visual-spec.md     # 视觉设计规格
│   ├── skills/                # 可复用的工作流
│   │   ├── brainstorming.md   # 头脑风暴流程
│   │   ├── component-creator.md
│   │   ├── web-design.md
│   │   └── page-creator.md
│   └── commands/              # 自定义命令
│       ├── commit.md          # 提交代码
│       └── plan.md            # 制定计划
└── src/
```

`<font style="color:rgb(25, 27, 31);background-color:rgb(248, 248, 250);">CLAUDE.md</font>`<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">常见内容：</font>

```plain
## 常用命令
...

## 技术栈
...

## 项目结构
...

## 架构概述
...

...

你必须 xxx
你不能 xxx
```

**<font style="color:rgb(25, 27, 31);">一开始让 AI 理解项目后自己生成这些文档，然后再人工进行详细的修改</font>**<font style="color:rgb(25, 27, 31);">。</font>

**<font style="color:rgb(25, 27, 31);">当项目调整时，更新文档。每次 AI 出错，就在文档中添加</font>****<font style="color:rgb(25, 27, 31);"> </font>**`**<font style="color:rgb(25, 27, 31);background-color:rgb(248, 248, 250);">你必须 xxx</font>**`**<font style="color:rgb(25, 27, 31);"> </font>****<font style="color:rgb(25, 27, 31);">等规则</font>**<font style="color:rgb(25, 27, 31);">，不要嫌麻烦，这可以大大减少让反复 AI 修改的次数。</font>

### <font style="color:rgb(25, 27, 31);">2. 任务编排：设计清晰的开发步骤</font>
**<font style="color:rgb(25, 27, 31);">不要直接让 AI 开发，必须先制定详细的计划。</font>**<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">有了明确的计划，AI 才会按照计划执行，之后你就可以放心让 AI 逐步完成任务。</font>

<font style="color:rgb(25, 27, 31);">在 Claude Code 中，连续按两次</font><font style="color:rgb(25, 27, 31);"> </font>`<font style="color:rgb(25, 27, 31);background-color:rgb(248, 248, 250);">Shift+Tab</font>`<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">进入 Plan 模式。在这个模式下，详细告诉 AI 你想要什么。如果你不清楚，可以让 AI 给你推荐方案。</font>

<font style="color:rgb(25, 27, 31);">但单单计划和执其实是不够的。真正的开发是一套闭环：</font>**<font style="color:rgb(25, 27, 31);">计划 → 执行 → 验收 → 不通过则重新执行 → 再验收</font>**<font style="color:rgb(25, 27, 31);">。</font>

<font style="color:rgb(25, 27, 31);">我推荐从开源的任务工作流开始，比如</font><font style="color:rgb(25, 27, 31);"> </font>[<font style="color:rgb(9, 64, 142);">superpowers</font>](https://link.zhihu.com/?target=https%3A//github.com/obra/superpowers)<font style="color:rgb(25, 27, 31);">。它有一套完整的任务编排逻辑：头脑风暴 → 制定计划 → 执行 → 验收 → 完成任务。</font>

<font style="color:rgb(25, 27, 31);">最后，当一个任务结束后，建议开始新的对话，避免上下文堆积影响后续任务。</font>

### <font style="color:rgb(25, 27, 31);">3. 自动化治理：长时间自主编码的前提</font>
<font style="color:rgb(25, 27, 31);">自动化治理是让 AI 长时间自主运行编码任务的前提。简单来讲，这是一套可以循环的工作流：</font>

1. **<font style="color:rgb(25, 27, 31);">规划</font>**<font style="color:rgb(25, 27, 31);">：AI 根据需求规划任务</font>
2. **<font style="color:rgb(25, 27, 31);">生成</font>**<font style="color:rgb(25, 27, 31);">：根据任务生成代码</font>
3. **<font style="color:rgb(25, 27, 31);">验证</font>**<font style="color:rgb(25, 27, 31);">：运行测试、检查代码</font>
4. **<font style="color:rgb(25, 27, 31);">修复</font>**<font style="color:rgb(25, 27, 31);">：检查并修复代码</font>
5. **<font style="color:rgb(25, 27, 31);">确认</font>**<font style="color:rgb(25, 27, 31);">：循环继续直到通过</font>

<font style="color:rgb(25, 27, 31);">Cursor 在博客</font><font style="color:rgb(25, 27, 31);"> </font>[<font style="color:rgb(9, 64, 142);">扩展长时间运行的自主编码能力</font>](https://link.zhihu.com/?target=https%3A//cursor.com/cn/blog/scaling-agents)<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">中分享了他们的实践：</font>

+ **<font style="color:rgb(25, 27, 31);">规划 Agent</font>**<font style="color:rgb(25, 27, 31);">：探索代码库并创建任务</font>
+ **<font style="color:rgb(25, 27, 31);">执行 Agent</font>**<font style="color:rgb(25, 27, 31);">：领取任务并专注于把任务完成到底</font>
+ **<font style="color:rgb(25, 27, 31);">评审 Agent</font>**<font style="color:rgb(25, 27, 31);">：判断任务是否完成，决定是否继续</font>

<font style="color:rgb(25, 27, 31);">单个 Agent 在执行专注的小任务时表现不错，但复杂项目需要多个 Agent 协同。多 Agent 协同目前还很难，但这是未来的方向。</font>

### <font style="color:rgb(25, 27, 31);">4. 能力沉淀：将经验转化为可复用的 Skills</font>
<font style="color:rgb(25, 27, 31);">最近 Agent Skills 非常火。简单来说，就是把个人经验用文字沉淀下来，交给 AI 来执行。</font>

<font style="color:rgb(25, 27, 31);">我认为 Skills 在未来会变得非常重要。举个例子：</font>[<font style="color:rgb(9, 64, 142);">Vercel</font>](https://zhida.zhihu.com/search?content_id=269143476&content_type=Article&match_order=1&q=Vercel&zhida_source=entity)<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">开源了一个</font><font style="color:rgb(25, 27, 31);"> </font>[<font style="color:rgb(9, 64, 142);">React 最佳实践的 Skills</font>](https://link.zhihu.com/?target=https%3A//github.com/vercel-labs/agent-skills/tree/main/packages/react-best-practices-build)<font style="color:rgb(25, 27, 31);">，这是一位十年经验大佬的技能沉淀——现在你可以直接拿去用了。</font>

<font style="color:rgb(25, 27, 31);">这就是 Skills 的魅力：</font>**<font style="color:rgb(25, 27, 31);">技能可以被复制和传递</font>**<font style="color:rgb(25, 27, 31);">。别人的经验写成 Skills，你通过 AI 就能获得这项技能。</font>

<font style="color:rgb(25, 27, 31);">作为项目开发者，你应该把熟悉的开发流程提炼成 Skills：项目的开发 SOP、组件创建规范、代码审查流程等等。这可以极大地解放重复劳动，交给 AI 来做。在 Claude Code 中，Skills 放在</font><font style="color:rgb(25, 27, 31);"> </font>`<font style="color:rgb(25, 27, 31);background-color:rgb(248, 248, 250);">.claude/skills/</font>`<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">目录下。</font>

<font style="color:rgb(25, 27, 31);">此外，</font>`<font style="color:rgb(25, 27, 31);background-color:rgb(248, 248, 250);">.claude/commands/</font>`<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">可以定义自定义命令，比如</font><font style="color:rgb(25, 27, 31);"> </font>`<font style="color:rgb(25, 27, 31);background-color:rgb(248, 248, 250);">/commit</font>`<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">自动提交代码、</font>`<font style="color:rgb(25, 27, 31);background-color:rgb(248, 248, 250);">/plan</font>`<font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">制定开发计划等，让常用操作一键触发。</font>

## <font style="color:rgb(25, 27, 31);">总结</font>
<font style="color:rgb(25, 27, 31);">看到这里，对于「面试问到你怎么看 Vibe Coding」这个问题，你应该心中有答案了：</font>**<font style="color:rgb(25, 27, 31);">文档化、任务编排、自动化治理、Skills 沉淀</font>**
