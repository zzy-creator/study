### LLM<font style="color:rgb(37, 39, 42);">（Large Language Model）</font>
<font style="color:rgb(37, 39, 42);">LLM 是一种基于深度学习的自然语言处理（NLP）</font>**<font style="color:rgb(37, 39, 42);">模型</font>**

<font style="color:rgb(37, 39, 42);">LLM 最经典的产品形态就是一问一答的 </font>`<font style="color:rgb(37, 39, 42);">chat 模式</font>`<font style="color:rgb(37, 39, 42);">。用户</font><u><font style="color:rgb(37, 39, 42);">输入一段文本</font></u><font style="color:rgb(37, 39, 42);">，模型会根据用户输入，</font><u><font style="color:rgb(37, 39, 42);">输出一段文本</font></u><font style="color:rgb(37, 39, 42);">。</font>

#### <font style="color:rgb(37, 39, 42);">token</font>
<font style="color:rgb(37, 39, 42);">Token 是模型对文本进行分割后的最小单元，可以是单词、子词（subword）、字符，甚至标点符号。</font>

+ <font style="color:rgb(37, 39, 42);">子词（subword）</font>
    - <font style="color:rgb(13, 18, 57);">指介于字符和词语之间的、具有语义意义的最小语言单位</font>
    - <font style="color:rgb(13, 18, 57);">例如</font><font style="color:rgb(112, 128, 144);background-color:rgb(245, 242, 240);">常见的词根/前缀/后缀</font>

<font style="color:rgb(37, 39, 42);">为什么需要 token</font>

+ 模型输入处理：模型无法直接理解原始文本，需将文本转化为数字序列（token ID），再通过 embedding 转换为向量进行计算。
+ 解决词汇量问题：直接按单词分会有大量罕见词（如专业术语），而子词分词（Subword Tokenization）能平衡常见词与罕见词。

#### <font style="color:rgb(37, 39, 42);">提示词(Prompt)</font>
在 LLM 中，提示词分为 2 类：  
1.System Prompt（系统提示词）：“你是一个资深的前端研发专家，....”;  
2.User Prompt（用户提示词）: "我有一个xxx 的问题，应该如何解决"；

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/jpeg/88656377/1766133872909-1669cedc-2514-4686-9065-9caedc72367c.jpeg" width="1690" title="" crop="0,0,1,1" id="ubaf03691" class="ne-image">

系统提示词是很有用的，他可以告诉LLM该去检索哪个领域的知识、规范回答的语言风格和用词、强化任务边界

#### LLM的限制
1. 幻觉；
2. <font style="color:rgb(37, 39, 42);">知识无法实时更新：LLM 掌握的知识截止到训练结束，比如问它今天发生的事情，它是无法知道的;</font>
3. 只能说，不能做。即使能力强大，依旧是一个 language 模型；

### Agent
#### Agent = LLM + Memory + Tools
<u><font style="color:rgb(37, 39, 42);">Agent 就是一种 LLM 的工程化落地方案</font></u><font style="color:rgb(37, 39, 42);">。通过工程手段去解决上述的LLM限制。</font>

| <font style="color:rgb(0, 52, 107);background-color:rgb(217, 234, 252);">关键组件</font> | <font style="color:rgb(0, 52, 107);background-color:rgb(217, 234, 252);">解释</font> | <font style="color:rgb(0, 52, 107);background-color:rgb(217, 234, 252);">实现方案</font> | <font style="color:rgb(0, 52, 107);background-color:rgb(217, 234, 252);">组件定位</font> |
| --- | --- | --- | --- |
| <font style="color:rgb(37, 39, 42);">大脑</font> | <font style="color:rgb(37, 39, 42);">负责理解任务、推理、规划和决策；</font> | <font style="color:rgb(37, 39, 42);">LLM；</font> | <font style="color:rgb(37, 39, 42);">最核心能力；</font> |
| <font style="color:rgb(37, 39, 42);">记忆</font><br/><font style="color:rgb(37, 39, 42);">Memory</font> | <font style="color:rgb(37, 39, 42);">用于存储和检索历史交互、经验、状态等信息；</font> | <font style="color:rgb(37, 39, 42);">短期记忆（上下文窗口）和长期记忆（向量数据库）</font> | <font style="color:rgb(37, 39, 42);">解决 LLM 上下文窗口大小限制;</font> |
| <font style="color:rgb(37, 39, 42);">工具</font><br/><font style="color:rgb(37, 39, 42);">Tools</font> | <font style="color:rgb(37, 39, 42);">与外部世界交互的手段，也是执行具体任务的载体；</font> | <font style="color:rgb(37, 39, 42);">API、数据库查询、代码执行、搜索、文件处理等各种功能模块</font> | <font style="color:rgb(37, 39, 42);">解决 LLM 只能说不能做的问题；</font> |


<font style="color:rgb(37, 39, 42);">2 类 Agent：</font>

| <font style="color:rgb(0, 52, 107);background-color:rgb(217, 234, 252);">名称</font> | <font style="color:rgb(0, 52, 107);background-color:rgb(217, 234, 252);">特点</font> | <font style="color:rgb(0, 52, 107);background-color:rgb(217, 234, 252);">区别</font> | |
| --- | --- | --- | --- |
| <font style="color:rgb(37, 39, 42);">fully autonomous systems</font><br/><font style="color:rgb(37, 39, 42);">（全自动系统）</font> | <font style="color:rgb(37, 39, 42);">长时间内独立运行，使用各种工具来完成复杂的任务；</font> | <font style="color:rgb(37, 39, 42);">大模型</font><u><font style="color:rgb(37, 39, 42);">动态决定</font></u><font style="color:rgb(37, 39, 42);">自己的流程及使用什么工具，</font><u><font style="color:rgb(37, 39, 42);">自主控制</font></u><font style="color:rgb(37, 39, 42);">如何完成任务 </font> | <img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/png/88656377/1766135409802-92f7aae9-3bcf-46c3-8637-9d6218713b11.png" width="852.8" title="" crop="0,0,1,1" id="uad81fad5" class="ne-image"> |
| <font style="color:rgb(37, 39, 42);">workflows</font><br/><font style="color:rgb(37, 39, 42);">（工作流）</font> | <font style="color:rgb(37, 39, 42);">follow predefined workflows（遵循预定义的工作流）</font> | <font style="color:rgb(37, 39, 42);">通过</font><u><font style="color:rgb(37, 39, 42);">预定义的代码路径</font></u><font style="color:rgb(37, 39, 42);">来编排大模型和和工具；</font> | <img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/png/88656377/1766135425101-43aacbcd-cbd2-4935-ba88-43bee3a9decc.png" width="1413.6" title="" crop="0,0,1,1" id="ub78f9e96" class="ne-image"> |


<font style="color:rgb(37, 39, 42);"></font>

#### 经典框架-ReAct（Reason + Act）
ReAct是智能体（Agent）处理复杂任务的核心框架，它通过动态推理与行动执行的循环，使Agent具备类似人类的“思考-行动-观察”能力。  
ReAct框架通过三步循环完成任务：  
1.推理（Reason）：分析当前状态，规划下一步行动。  
2.行动（Act）：调用工具或执行操作（如API调用、代码执行）。  
3.观察（Observe）：获取行动结果，更新上下文，进入下一轮循环



#### 如何判断一个业务功能是否可以用 Agent 来实现？
+ 如果没有 Agent，这个业务问题能不能靠人自己来解决？  
1.如果能够解决，那么 Agent / workflow 可以帮助我们把流程自动化；  
2.如果解决不了，那么 Agent / workflow 大概率也解决不了我们的问题；

#### 何时使用 Agent / workflows ?
+ 使用最简单可行的方式达到目的  
1.如果提示词能解决，就用提示词；  
2.如果自动化工作流（workflow)能解决，就用工作流；  
3.如果 Agent 能解决，就用 Agent;
