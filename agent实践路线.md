从0到复刻基础项目：3个月；到进阶项目：6个月

先考虑前端+AI agent调用的岗位，不是完全的AI AGENT工程师。所以有agent项目经历，解决过一些个难点即可。

[https://www.zhihu.com/question/14128984016/answer/117852908852](https://www.zhihu.com/question/14128984016/answer/117852908852)

[https://www.zhihu.com/people/zhao-yu-xiang-9-99](https://www.zhihu.com/people/zhao-yu-xiang-9-99)

+ 学习路线：[https://www.zhihu.com/question/1936375725931361485/answer/2004853008891131464](https://www.zhihu.com/question/1936375725931361485/answer/2004853008891131464)
+ 具体的会遇到的、需要去攻克的、学习了解的痛点难点：[https://www.zhihu.com/question/1936375725931361485/answer/1948826620803657995](https://www.zhihu.com/question/1936375725931361485/answer/1948826620803657995)
+ 开源项目推荐：[https://www.zhihu.com/question/14128984016/answer/117852908852](https://www.zhihu.com/question/14128984016/answer/117852908852)
+ <font style="color:rgb(25, 27, 31);">Anthropic学习路径官方文章：</font>[https://zhuanlan.zhihu.com/p/1994463393139151039](https://zhuanlan.zhihu.com/p/1994463393139151039)



ata上面讲agent等概念讲的很清楚的文章X2，并都有相应的源码：

+ [https://ata.atatech.org/articles/12020460408?spm=ata.23639746.0.0.57a65d97ph9kqP#OWJjMGMy](https://ata.atatech.org/articles/12020460408?spm=ata.23639746.0.0.57a65d97ph9kqP#OWJjMGMy)
+ [https://ata.atatech.org/articles/12020590911?spm=ata.21736010.0.0.5ebe75365dJUX6#ZjlmODI2](https://ata.atatech.org/articles/12020590911?spm=ata.21736010.0.0.5ebe75365dJUX6#ZjlmODI2)

  
<font style="color:rgb(25, 27, 31);">先自己手写一个简单的 Agent，然后再学习框架</font>**<font style="color:rgb(25, 27, 31);">LangChain</font>**<font style="color:rgb(25, 27, 31);"> (JavaScript/Python)</font>

<font style="color:rgb(25, 27, 31);"></font>

**<font style="color:rgb(25, 27, 31);"> LLM API</font>**<font style="color:rgb(25, 27, 31);"> 选择： 我用的是 Claude API，文档清晰，Tool Calling 支持好。OpenAI 也不错，看个人喜好。</font>

<font style="color:rgb(25, 27, 31);"></font>

<font style="color:rgb(25, 27, 31);"></font>

### <font style="color:rgb(25, 27, 31);">RAG</font>
<font style="color:rgb(18, 18, 18);">每当将大模型应用于实际业务场景时发现，通用的基础大模型基本无法满足实际业务需求，主要有以下几方面原因：</font>

+ **<font style="color:rgb(18, 18, 18);">知识的局限性</font>**<font style="color:rgb(18, 18, 18);">：大模型自身的知识完全源于训练数据，而现有的主流大模型（deepseek、文心一言、通义千问…）的训练集基本都是构建于网络公开的数据，对于一些实时性的、非公开的或私域的数据是没有。</font>
+ **<font style="color:rgb(18, 18, 18);">幻觉问题</font>**<font style="color:rgb(18, 18, 18);">：所有的深度学习模型的底层原理都是基于数学概率，模型输出实质上是一系列数值运算，大模型也不例外，所以它经常会一本正经地胡说八道，尤其是在大模型自身不具备某一方面的知识或不擅长的任务场景。</font>
+ **<font style="color:rgb(18, 18, 18);">数据安全性</font>**<font style="color:rgb(18, 18, 18);">：对于企业来说，数据安全至关重要，没有企业愿意承担数据泄露的风险，尤其是大公司，没有人将私域数据上传第三方平台进行训练会推理。这也导致完全依赖通用大模型自身能力的应用方案不得不在数据安全和效果方面进行取舍。</font>

<font style="color:rgb(18, 18, 18);">而RAG就是解决上述问题的有效方案。</font>

<font style="color:rgb(71, 71, 71);"></font>

<font style="color:rgb(71, 71, 71);">RAG用于为LLM补充私有或专有数据信息</font>

<font style="color:rgb(37, 39, 42);">RAG是Retrieval Augmentation Generation三个词的缩写，代表了三个核心的行为</font>**<font style="color:rgb(37, 39, 42);">Retrieve-检索、Augment-增强以及Generate-生成</font>**<font style="color:rgb(37, 39, 42);">，同时在三个核心动作之外，还有一个</font>**<font style="color:rgb(37, 39, 42);">embedding-编码</font>**<font style="color:rgb(37, 39, 42);">。</font>

<font style="color:rgb(37, 39, 42);"></font>

<font style="color:rgb(37, 39, 42);">RAG核心的功能就是</font>**<font style="color:rgb(37, 39, 42);">针对用户Query，补充和Query相关的且模型没有的信息</font>**<font style="color:rgb(37, 39, 42);">，同时要在两个维度上做要求：1. </font>**<font style="color:rgb(37, 39, 42);">召回率</font>**<font style="color:rgb(37, 39, 42);">：能够找到最相关的信息；2.</font>**<font style="color:rgb(37, 39, 42);">精确率</font>**<font style="color:rgb(37, 39, 42);">：不相关的信息不要；RAG技术以及我们针对实践的设计，主要就是锚定这两个维度指标的提升去的，同时这两个指标在现实实践中是个权衡，需要找到一个相对适合的值，追求两者都很高，不太现实，或者说可能需要付出的代价不足以让我们这么去做；</font>

<font style="color:rgb(18, 18, 18);">RAG的核心理解为“检索+生成”，前者主要是利用向量数据库的高效存储和检索能力，召回目标知识；后者则是利用大模型和Prompt工程，将召回的知识合理利用，生成目标答案。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2026/png/88656377/1772703454163-c0c94b46-4a90-490a-87a1-ada0f68a9f6f.png" width="668" title="" crop="0,0,1,1" id="u64106797" class="ne-image">

### 2月：打基础
**Week 1：理解 LLM**

+ 注册 LLM API: Claude / OpenAI API，写第一个调用
+ 理解 Token、Temperature、Max Tokens 等参数
+ 尝试不同的 Prompt，看效果差异

**Week 2：实现 Tool Calling**

+ 手写一个简单的 Agent（支持2-3个工具）
+ 工具示例：天气查询、网页搜

### 3月：深入实战
**Week 3-4：学习 RAG**

+ 理解向量数据库（我用的是 Pinecone 和 Chroma）
+ 实现一个基于文档的问答系统
+ 不能只是调用API，要理解LLM的能力边界和工作原理
    - <font style="color:rgb(25, 27, 31);">不用理解 Transformer 的每一个数学细节</font>
    - 什么是 Embedding？为什么需要向量数据库？Cosine Similarity 到底在算个啥？RAG（检索增强生成）的本质是什么？[ReAct](https://zhida.zhihu.com/search?content_id=746271455&content_type=Answer&match_order=1&q=ReAct&zhida_source=entity)（Reasoning and Acting）这个模式是怎么让 LLM 和外部工具交互的？Function Calling 的工作流程是怎样的？
+ **2、动手写一个“丐版”的 RAG。（暂时不做）**

别上来就用 LangChain。你自己用 `sentence-transformers` 库把文档切块、生成向量，存到一个 [Faiss](https://zhida.zhihu.com/search?content_id=746271455&content_type=Answer&match_order=1&q=Faiss&zhida_source=entity) 或者 ChromaDB 的本地实例里。然后用户提问时，你手动去查向量库，把查出来的文本拼到 Prompt 里，再去调 OpenAI 的 API。这个过程跑一遍，你对 RAG 的理解会比看一百个教程都深刻。你会立刻遇到问题：文档怎么切分效果最好？Top-K 设成多少合适？搜出来的东西不相关怎么办？——恭喜你，你已经开始接触 Agent 工程的真正难点了。

**Week 5-6：部署到生产环境**

+ 在[英博云平台](https://link.zhihu.com/?target=https%3A//www.ebcloud.com/chn_a6mfbgsc)部署第一个 Agent
+ 学习如何处理并发请求
+ 实现用户认证和 API 限流

### 4月：进阶优化
**Week 9-10：优化性能和成本**

+ 学习 Prompt Caching（减少 Token 消耗）
+ 实现流式输出（Streaming）
+ 优化工具调用的准确率

**Week 11-12：构建完整应用**

+ 前端 + 后端 + Agent 的完整应用
+ 我用 Next.js + FastAPI + Claude API

部署并优化、观测、监控

+ 部署到[英博云平台](https://link.zhihu.com/?target=https%3A//www.ebcloud.com/chn_a6mfbgsc)
+ **1、成本和延迟意识**

你得知道，LLM API 是按 token 烧钱的。一个设计不好的 Agent 链条，一个请求进来可能要来回调用 LLM 十几次，成本直接爆炸。你怎么设计缓存策略？怎么通过更小的模型（比如 fine-tune 一个本地模型）来处理某些固定任务？怎么优化 Prompt 来减少 token 消耗？这些都是 P7 级别需要考虑的问题。

**2、可观测性（Observability）**

一个 Agent 的执行过程是个复杂的黑盒。你需要引入像 `[LangSmith](https://zhida.zhihu.com/search?content_id=746271455&content_type=Answer&match_order=1&q=LangSmith&zhida_source=entity)`、`[wandb](https://zhida.zhihu.com/search?content_id=746271455&content_type=Answer&match_order=1&q=wandb&zhida_source=entity)` 这样的工具，去追踪每一次调用的 Prompt、返回结果、中间步骤、token 消耗。线上出了问题，你得能快速复盘是哪个环节掉链子了。



MORE（暂时不做，了解下就行）：

+ **<font style="color:rgb(25, 27, 31);">Multi-Agent 系统</font>**<font style="color:rgb(25, 27, 31);">：多个 Agent 协作完成任务</font>
+ **<font style="color:rgb(25, 27, 31);">Agent 评估</font>**<font style="color:rgb(25, 27, 31);">：如何量化 Agent 的表现</font>
+ **<font style="color:rgb(25, 27, 31);">Fine-tuning</font>**<font style="color:rgb(25, 27, 31);">：针对特定任务微调模型</font>



+ <font style="color:rgb(25, 27, 31);">用 React/Vue 构建 Chat UI</font>
+ <font style="color:rgb(25, 27, 31);">用 WebSocket 实现流式输出</font>
+ <font style="color:rgb(25, 27, 31);">用 Next.js 做全栈 Agent 应用</font>

<font style="color:rgb(25, 27, 31);"></font>

### <font style="color:rgb(25, 27, 31);">心得</font>
Embedding 是一种将非结构化数据（如文本、图像、音频）转化为计算机可理解和处理的数值向量（一组数字）的技术。 这种转换的核心思想是：语义上相似的数据，在向量空间中的位置也相近。



Node.js 本质是一个 JS 运行环境让 JS 能脱离浏览器运行可以用在很多地方，不只是服务端



temperature没什么大用，调高后会出现回答的上下token不匹配、连接不顺畅。要控制在1.2内。

因为现在<font style="color:rgb(13, 18, 57);background-color:rgb(246, 247, 248);">没有模型能做到真正的"全局规划后再输出"，所有模型本质上都是逐token生成的</font>

<font style="color:rgb(13, 18, 57);background-color:rgb(246, 247, 248);"></font>

<font style="color:rgb(13, 18, 57);background-color:rgb(246, 247, 248);">兜底操作、兜底值应该在逻辑处理代码里设置、处理，不要想着提示了LLM要兜底，他就一定会传参兜底参数之类的。</font>
