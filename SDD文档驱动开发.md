**AI是概率输出结果的，所以给他具体详细的步骤，每一步人工确认输出的东西，最终产物的正确性就可以大大提升**
**长时间对话，积累上下文，会让ai有幻觉，不知道对话中哪个是正确的。所以用spec，就保证了ai可以拥有正确的事实源**

编写需求spec->反复确认&让agent修改spec直至满意->让agent输出技术设计到spec（也就是具体要在哪个文件、哪个地方怎么进行改动）->确认无误后，执行写代码->写完让agent根据spec review自己写的代码  


step0：安装已有的SDD skill，以下的步骤其实就是SDD SKILL的思路

### <font style="color:rgba(25, 26, 31, 0.9);">Step 1: 明确需求。Research (调研与意图锁定)</font>
**<font style="color:rgba(25, 26, 31, 0.9);">“不要急着给方案，先搞清楚到底要解决什么问题。”</font>**<font style="color:rgba(25, 26, 31, 0.9);">  
</font><font style="color:rgba(25, 26, 31, 0.9);">很多时候，我们的需求描述是模糊的。这个阶段的核心是</font><font style="color:rgba(25, 26, 31, 0.9);"> </font>**<font style="color:rgba(25, 26, 31, 0.9);">“反向复述”</font>**<font style="color:rgba(25, 26, 31, 0.9);">。</font>

+ **<font style="color:rgba(25, 26, 31, 0.9);">输入</font>**<font style="color:rgba(25, 26, 31, 0.9);">：你模糊的想法、Bug 的现象、或者一段杂乱的聊天记录。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">动作</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    1. **<font style="color:rgba(25, 26, 31, 0.9);">让 AI 阅读并复述</font>**<font style="color:rgba(25, 26, 31, 0.9);">：指令它 —— </font>_<font style="color:rgba(25, 26, 31, 0.9);">“请阅读上述需求，用你自己的话复述一遍，并指出其中不清晰的地方。”</font>_
    2. **<font style="color:rgba(25, 26, 31, 0.9);">澄清边界</font>**<font style="color:rgba(25, 26, 31, 0.9);">：让 AI 告诉你，这个需求涉及哪些业务领域？需要参考哪些现有的代码逻辑？</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">产出</font>**<font style="color:rgba(25, 26, 31, 0.9);">：清晰的 </font>**<font style="color:rgba(25, 26, 31, 0.9);">Requirement Spec</font>**<font style="color:rgba(25, 26, 31, 0.9);"> (需求意图)。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">🚪</font>****<font style="color:rgba(25, 26, 31, 0.9);"> 验收门禁</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    - _<font style="color:rgba(25, 26, 31, 0.9);">AI 指出的“模糊点”是否都已解答？AI是不是已经完全明白了需求意图和项目结构？</font>_

### <font style="color:rgba(25, 26, 31, 0.9);">Step 2: 明确技术方案。Innovate (设计与推演)</font>
**<font style="color:rgba(25, 26, 31, 0.9);">“这是体现架构师价值的环节。寻找最优解，而不是第一个想到的解。”</font>**<font style="color:rgba(25, 26, 31, 0.9);">  
</font><font style="color:rgba(25, 26, 31, 0.9);">这一步严禁写代码，而是要进行</font><font style="color:rgba(25, 26, 31, 0.9);"> </font>**<font style="color:rgba(25, 26, 31, 0.9);">“审讯游戏 (The Interrogation Game)”</font>**<font style="color:rgba(25, 26, 31, 0.9);">。</font>

+ **<font style="color:rgba(25, 26, 31, 0.9);">动作</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    1. **<font style="color:rgba(25, 26, 31, 0.9);">生成草案</font>**<font style="color:rgba(25, 26, 31, 0.9);">：让 AI 根据需求整理一份《技术实施草案》 (HLD)。</font>
    2. **<font style="color:rgba(25, 26, 31, 0.9);">强制“互问互答”</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
        * **<font style="color:rgba(25, 26, 31, 0.9);">你要问它</font>**<font style="color:rgba(25, 26, 31, 0.9);">：“除了这个方案，还有没有更好的？”“这样做的坏处是什么？”</font>
        * **<font style="color:rgba(25, 26, 31, 0.9);">逼它问你</font>**<font style="color:rgba(25, 26, 31, 0.9);">：指令它 —— </font>_<font style="color:rgba(25, 26, 31, 0.9);">“如果你对现有业务逻辑或代码细节有任何不确定的地方，请立刻向我提问，不要自己  
</font>__<font style="color:rgba(25, 26, 31, 0.9);">瞎猜（Hallucinate）。”</font>_
    3. **<font style="color:rgba(25, 26, 31, 0.9);">引入外部智慧</font>**<font style="color:rgba(25, 26, 31, 0.9);">：把你同事的建议，或者你在其他项目的经验喂给它作为补充。</font>

_<font style="color:rgba(25, 26, 31, 0.9);">💡</font>__<font style="color:rgba(25, 26, 31, 0.9);"> Pro Tip：去拟人化交互 (De-anthropomorphism)  
</font>__<font style="color:rgba(25, 26, 31, 0.9);">在向 AI 索要方案时，千万不要用“你” (You)。记住：不要问它“怎么看”，要问它“它模拟的那个专家角色”怎么看。例如：顶尖专家和学者将会如何修改这个bug；或者顶尖程序员和架构师将如何设计这个功能等。</font>_

+ **<font style="color:rgba(25, 26, 31, 0.9);">产出</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>**<font style="color:rgba(25, 26, 31, 0.9);">Design Spec</font>**<font style="color:rgba(25, 26, 31, 0.9);"> (设计/技术规格书)，包含核心技术选型、Pros/Cons 分析。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">🚪</font>****<font style="color:rgba(25, 26, 31, 0.9);"> 验收门禁</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    - _<font style="color:rgba(25, 26, 31, 0.9);">你是否对这个设计方案进行了 review和Sign-off（批准）？</font>_

### <font style="color:rgba(25, 26, 31, 0.9);">Step 3: 明确技术详细实施计划。Plan (规划与契约)</font>
**<font style="color:rgba(25, 26, 31, 0.9);">“从战略下沉到战术。不仅要告诉它造什么房子，还要告诉它每一块砖怎么砌。”</font>**<font style="color:rgba(25, 26, 31, 0.9);">  
</font><font style="color:rgba(25, 26, 31, 0.9);">文档即协议。我们要把模糊的 Design 变成精确的 Implementation Plan。</font>

+ **<font style="color:rgba(25, 26, 31, 0.9);">动作</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    1. **<font style="color:rgba(25, 26, 31, 0.9);">明确物理路径</font>**<font style="color:rgba(25, 26, 31, 0.9);">：Spec 里必须写清楚：</font>
        * <font style="color:rgba(25, 26, 31, 0.9);">要修改哪几个文件（File Paths）？</font>
        * <font style="color:rgba(25, 26, 31, 0.9);">要新增哪几个方法和类（Signatures）？</font>
        * **<font style="color:rgba(25, 26, 31, 0.9);">Mock 数据</font>**<font style="color:rgba(25, 26, 31, 0.9);">：在写代码前，先定义好接口的 Request/Response 示例。</font>
    2. **<font style="color:rgba(25, 26, 31, 0.9);">认知对齐</font>**<font style="color:rgba(25, 26, 31, 0.9);">：再次进行 Review。问它：“为什么要在 Service 层做这个校验，而不是 Controller 层？”确保它不是在套模板，而是真的理解了逻辑。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">产出</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>**<font style="color:rgba(25, 26, 31, 0.9);">Implementation Spec</font>**<font style="color:rgba(25, 26, 31, 0.9);"> (详细实施/接口文档)。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">🚪</font>****<font style="color:rgba(25, 26, 31, 0.9);"> 验收门禁</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    - _<font style="color:rgba(25, 26, 31, 0.9);">实施计划是否拆解到了“原子级”任务，如果换一个大模型是否可以100%完美实施？</font>_

### <font style="color:rgba(25, 26, 31, 0.9);">Step 4: Execute (执行与编码)</font>
**<font style="color:rgba(25, 26, 31, 0.9);">“你不是在看戏，你是在跟 AI 结对编程 (Pair Programming)。”</font>**

+ **<font style="color:rgba(25, 26, 31, 0.9);">动作</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    1. **<font style="color:rgba(25, 26, 31, 0.9);">分步指令</font>**<font style="color:rgba(25, 26, 31, 0.9);">：不要试图一次生成 500 行代码。按照 Plan 的步骤，一步一步来。</font>
        * _<font style="color:rgba(25, 26, 31, 0.9);">“好的，先完成 Step 1 的数据库 Schema 变更。”</font>_
        * _<font style="color:rgba(25, 26, 31, 0.9);">“现在进行 Step 2，实现 Service 层逻辑。”</font>_
    2. **<font style="color:rgba(25, 26, 31, 0.9);">实时自检</font>**<font style="color:rgba(25, 26, 31, 0.9);"> (Step-by-Step Check)：每做完一步，让 AI 自己总结：“我完成了什么，这是否符合 Spec 的要求？”</font>
    3. **<font style="color:rgba(25, 26, 31, 0.9);">人工干预</font>**<font style="color:rgba(25, 26, 31, 0.9);">：如果发现它跑偏了，</font>**<font style="color:rgba(25, 26, 31, 0.9);">立刻暂停</font>**<font style="color:rgba(25, 26, 31, 0.9);">。不要在原来的基础上打补丁，而是回滚这一步，修正 Prompt 后重试。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">产出</font>**<font style="color:rgba(25, 26, 31, 0.9);">：源代码。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">🚪</font>****<font style="color:rgba(25, 26, 31, 0.9);"> 硬性门禁</font>**<font style="color:rgba(25, 26, 31, 0.9);"> (Hard Gates)：</font>
    - _**<font style="color:rgba(25, 26, 31, 0.9);">Lint Check</font>**__<font style="color:rgba(25, 26, 31, 0.9);">：生成的代码必须通过 Linter 检查（无语法错误、无未使用的变量）。</font>_
    - _**<font style="color:rgba(25, 26, 31, 0.9);">Compile Check</font>**__<font style="color:rgba(25, 26, 31, 0.9);">：代码必须能编译通过。如果跑不通，严禁进入下一步。</font>_

### <font style="color:rgba(25, 26, 31, 0.9);">Step 5: Review (验收与对齐)</font>
<font style="color:rgba(25, 26, 31, 0.9);">“让一个 AI 去检查另一个 AI 的作业。”</font>

_<font style="color:rgba(25, 26, 31, 0.9);">“这是对抗‘代码通胀’的唯一防线。当 Diff 达到几千行时，不要试图人肉 Review，要相信 Spec 的验证能力。”</font>_

+ **<font style="color:rgba(25, 26, 31, 0.9);">动作</font>**<font style="color:rgba(25, 26, 31, 0.9);">：</font>
    1. **<font style="color:rgba(25, 26, 31, 0.9);">New Chat / New Model</font>**<font style="color:rgba(25, 26, 31, 0.9);">：实施完成后，</font>**<font style="color:rgba(25, 26, 31, 0.9);">开启一个新的对话窗口</font>**<font style="color:rgba(25, 26, 31, 0.9);">，甚至换一个模型（比如用 Claude Review GPT 的代码）。</font>
    2. **<font style="color:rgba(25, 26, 31, 0.9);">法医式审查</font>**<font style="color:rgba(25, 26, 31, 0.9);">：把 </font>**<font style="color:rgba(25, 26, 31, 0.9);">Spec 文档</font>**<font style="color:rgba(25, 26, 31, 0.9);"> 和 </font>**<font style="color:rgba(25, 26, 31, 0.9);">Git Diff</font>**<font style="color:rgba(25, 26, 31, 0.9);"> 喂给新 AI。</font>
        * <font style="color:rgba(25, 26, 31, 0.9);">指令：</font>_<font style="color:rgba(25, 26, 31, 0.9);">“请基于这份 Spec 审查这次代码变更。寻找潜在 Bug、逻辑漏洞或不符合规范的地方。”</font>_
    3. **<font style="color:rgba(25, 26, 31, 0.9);">迭代修正</font>**<font style="color:rgba(25, 26, 31, 0.9);">：把审查报告扔回给负责写的 AI，让它解释并修正。如此循环几次，直到“评审官”满意。</font>
    4. **<font style="color:rgba(25, 26, 31, 0.9);">旁观者视角</font>**<font style="color:rgba(25, 26, 31, 0.9);"> </font><font style="color:rgba(25, 26, 31, 0.9);">(The Spectator Stance):  
</font><font style="color:rgba(25, 26, 31, 0.9);">不要问 AI：“你觉得刚才写的代码对吗？”（它通常会说“是对的”来讨好你）。  
</font><font style="color:rgba(25, 26, 31, 0.9);">要这样问：“如果请 Google 的 Principal Engineer 来做 Code Review，他会指出这段代码的哪些隐患？”  
</font><font style="color:rgba(25, 26, 31, 0.9);">通过引入第三方权威视角，可以有效打破模型的“顺从性幻觉”，强制它开启高强度的批判性思维。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">产出</font>**<font style="color:rgba(25, 26, 31, 0.9);">：单元测试、Review 报告、最终交付代码。</font>
+ **<font style="color:rgba(25, 26, 31, 0.9);">🚪</font>****<font style="color:rgba(25, 26, 31, 0.9);"> 硬性门禁</font>**<font style="color:rgba(25, 26, 31, 0.9);"> (Hard Gates)：</font>
    - _**<font style="color:rgba(25, 26, 31, 0.9);">Automated Tests</font>**__<font style="color:rgba(25, 26, 31, 0.9);">：自动化测试必须全绿（覆盖门槛按项目等级设定，并在 CI/规则库中固化）。</font>_
    - _**<font style="color:rgba(25, 26, 31, 0.9);">Interface Contract</font>**__<font style="color:rgba(25, 26, 31, 0.9);">：新代码的接口响应必须与</font>__<font style="color:rgba(25, 26, 31, 0.9);"> </font>_`_<font style="color:rgba(25, 26, 31, 0.9);background-color:rgba(27, 31, 35, 0.05);">02_interface.md</font>_`_<font style="color:rgba(25, 26, 31, 0.9);"> </font>__<font style="color:rgba(25, 26, 31, 0.9);">定义的 JSON Schema 完全一致（使用工具自动比对）。</font>_
    - _**<font style="color:rgba(25, 26, 31, 0.9);">未过门禁 = 0 交付</font>**__<font style="color:rgba(25, 26, 31, 0.9);">：任何一项失败，直接退回 Step 4，严禁合并代码。</font>_







迭代过程中，始终维护一个版本的**<font style="color:rgba(25, 26, 31, 0.9);">Requirement Spec</font>**（最新的）。功能改动在changelog里记录。bugfix无需记录（因为没有变更功能，spec不需要更新）
