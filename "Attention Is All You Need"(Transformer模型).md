详解：[https://zhuanlan.zhihu.com/p/569527564](https://zhuanlan.zhihu.com/p/569527564)

大概：[https://cloud.tencent.com/developer/article/2407712](https://cloud.tencent.com/developer/article/2407712)

### <font style="color:rgb(51, 51, 51);">背景</font>
<font style="color:rgb(51, 51, 51);">"Attention Is All You Need"是一篇于2017年发表的开创性论文，首次介绍了Transformer模型。</font>

**<font style="color:rgb(51, 51, 51);">这篇论文彻底改变了</font>**[**<font style="color:rgb(0, 82, 217);">自然语言处理</font>**](https://cloud.tencent.com/product/nlp?from_column=20065&from=20065)**<font style="color:rgb(51, 51, 51);">（NLP）领域的研究方向，为后续的众多NLP模型和应用奠定了基础。</font>**

+ <font style="color:rgb(25, 27, 31);">当时最好的架构是基于注意力的"encoder-decoder"架构。这些架构都使用了CNN或RNN。这篇文章提出的Transformer架构仅使用了注意力机制，而无需使用CNN和RNN。</font>
+ <font style="color:rgb(25, 27, 31);">两项机器翻译的实验表明，这种架构不仅精度高，而且训练时间大幅缩短。</font>

<font style="color:rgb(25, 27, 31);"></font>

### <font style="color:rgb(25, 27, 31);">知识储备</font>
<font style="color:rgb(25, 27, 31);">机器翻译，就是将某种语言的一段文字翻译成另一段文字。</font>

<font style="color:rgb(25, 27, 31);">由于翻译没有唯一的正确答案，用准确率来衡量一个机器翻译算法并不合适。因此，机器翻译的数据集通常会为每一条输入准备若干个参考输出。统计算法输出和参考输出之间的重复程度，就能评价算法输出的好坏了。这种评价指标叫做BLEU Score。这一指标越高越好。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/png/88656377/1764234171222-0f1e9be1-ae57-4dbf-9479-96ddc309d9e3.png" width="694" title="" crop="0,0,1,1" id="u57db2482" class="ne-image" style="color: rgb(25, 27, 31)">

<font style="color:rgb(25, 27, 31);">在深度学习时代早期，人们使用</font>[<font style="color:rgb(9, 64, 142);">RNN</font>](https://zhida.zhihu.com/search?content_id=214694629&content_type=Article&match_order=1&q=RNN&zhida_source=entity)<font style="color:rgb(25, 27, 31);">（循环神经网络）来处理机器翻译任务。一段输入先是会被预处理成一个token序列。RNN会对每个token逐个做计算，并维护一个表示整段文字整体信息的状态。根据当前时刻的状态，RNN可以输出当前时刻的一个token。</font>

<font style="color:rgb(83, 88, 97);">所谓token，既可以是一个单词、一个汉字，也可能是一个表示空白字符、未知字符、句首字符的特殊字符。  
</font>

<font style="color:rgb(25, 27, 31);">具体来说，在第</font><font style="color:rgb(25, 27, 31);">轮计算中，输入是上一轮的状态</font><font style="color:rgb(25, 27, 31);">以及这一轮的输入token</font><font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">，输出这一轮的状态</font><font style="color:rgb(25, 27, 31);">以及这一轮的输出token</font><font style="color:rgb(25, 27, 31);"> </font><font style="color:rgb(25, 27, 31);">。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/webp/88656377/1764234172719-7321777e-bf41-49c5-9b75-e6f96de6be2a.webp" width="565" title="" crop="0,0,1,1" id="u5be5e9aa" class="ne-image" style="color: rgb(25, 27, 31)">

<font style="color:rgb(25, 27, 31);">这种简单的RNN架构仅适用于输入和输出等长的任务。然而，大多数情况下，机器翻译的输出和输入都不是等长的。因此，人们使用了一种新的架构。前半部分的RNN只有输入，后半部分的RNN只有输出（上一轮的输出会当作下一轮的输入以补充信息）。两个部分通过一个状态</font><font style="color:rgb(25, 27, 31);">来传递信息。把该状态看成输入信息的一种编码的话，前半部分可以叫做“编码器”，后半部分可以叫做“解码器”。这种架构因而被称为“</font>[<font style="color:rgb(9, 64, 142);">编码器-解码器</font>](https://zhida.zhihu.com/search?content_id=214694629&content_type=Article&match_order=1&q=%E7%BC%96%E7%A0%81%E5%99%A8-%E8%A7%A3%E7%A0%81%E5%99%A8&zhida_source=entity)<font style="color:rgb(25, 27, 31);">”架构。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/png/88656377/1764234171138-dde606b3-67cc-4e4b-a3c6-49be873b9970.png" width="742" title="" crop="0,0,1,1" id="u57e49d82" class="ne-image" style="color: rgb(25, 27, 31)">

<font style="color:rgb(25, 27, 31);">这种架构存在不足：编码器和解码器之间只通过一个隐状态来传递信息。在处理较长的文章时，这种架构的表现不够理想。为此，有人提出了基于注意力的架构。这种架构依然使用了编码器和解码器，只不过解码器的输入是编码器的状态的加权和，而不再是一个简单的中间状态。每一个输出对每一个输入的权重叫做注意力，注意力的大小取决于输出和输入的相关关系。这种架构优化了编码器和解码器之间的信息交流方式，在处理长文章时更加有效。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/png/88656377/1764234170897-4eb189ff-6e1f-4c12-a422-042ee6d57e24.png" width="1023" title="" crop="0,0,1,1" id="u04e2eaf3" class="ne-image" style="color: rgb(25, 27, 31)">

<font style="color:rgb(25, 27, 31);">尽管注意力模型的表现已经足够优秀，但所有基于RNN的模型都面临着同样一个问题：RNN本轮的输入状态取决于上一轮的输出状态，这使RNN的计算必须串行执行。因此，RNN的训练通常比较缓慢。</font>

<font style="color:rgb(25, 27, 31);">在这一背景下，抛弃RNN，只使用</font>[<font style="color:rgb(9, 64, 142);">注意力机制</font>](https://zhida.zhihu.com/search?content_id=214694629&content_type=Article&match_order=1&q=%E6%B3%A8%E6%84%8F%E5%8A%9B%E6%9C%BA%E5%88%B6&zhida_source=entity)<font style="color:rgb(25, 27, 31);">的Transformer横空出世了。</font>

<font style="color:rgb(25, 27, 31);"></font>

### <font style="color:rgb(25, 27, 31);">模型</font>
<img src="https://intranetproxy.alipay.com/skylark/lark/0/2025/png/88656377/1764234945117-f6e3c44a-8b43-48b7-972c-ad81057d526f.png" width="606" title="" crop="0,0,1,1" id="uc9a507e0" class="ne-image">

#### 总结
该模型基于encoder-decoder的结构，摒弃了RNN，采用自注意力机制来学习序列中每个元素与其他元素的关联度，<font style="color:rgb(25, 27, 31);">提取出对序列更有意义的表示。</font>

encoder：对于输入，经过自注意力机制和其他处理，获得一个对输入的总体的表示

decoder：<font style="color:rgb(25, 27, 31);">输入当前已经解码的序列，经过自注意力机制和其他处理，获得一个对当前解码序列的总体的表示（masked是为了在接下来的计算里，遮掩输入单词里，当前位置之后的位置（翻译当前单词时，不应该知道后面位置的信息）），和输入序列计算注意力（找到每一个输出单词最相关的某几个输入单词），然后用注意力加权和算出输出。</font>

<font style="color:rgb(25, 27, 31);"></font>

<font style="color:rgb(51, 51, 51);">Transformer模型的核心设计理念可以概括为以下几点：</font>

#### **<font style="color:rgb(0, 0, 0);">1. 自注意力（Self-Attention）机制</font>**
+ **<font style="color:rgb(51, 51, 51);">核心概念</font>**<font style="color:rgb(51, 51, 51);">：Transformer模型的基础是自注意力机制，它允许模型在处理序列（如文本）时，</font>**<font style="color:rgb(51, 51, 51);">对序列中的每个元素计算其与序列中其他元素的关联度</font>**<font style="color:rgb(51, 51, 51);">。</font>**<font style="color:rgb(51, 51, 51);">这种机制使得模型能够捕捉到序列内长距离依赖关系</font>**<font style="color:rgb(51, 51, 51);">。</font>
+ **<font style="color:rgb(51, 51, 51);">优势</font>**<font style="color:rgb(51, 51, 51);">：相比于之前的RNN和LSTM，自注意力机制能够在</font>**<font style="color:rgb(51, 51, 51);">并行处理</font>**<font style="color:rgb(51, 51, 51);">时有效地处理长距离依赖问题，显著提高了处理速度和效率。</font>

#### **<font style="color:rgb(0, 0, 0);">2. 多头注意力（Multi-Head Attention）</font>**
+ **<font style="color:rgb(51, 51, 51);">设计</font>**<font style="color:rgb(51, 51, 51);">：在自注意力的基础上，Transformer引入了</font>**<font style="color:rgb(51, 51, 51);">多头注意力</font>**<font style="color:rgb(51, 51, 51);">机制，</font><font style="color:rgb(25, 27, 31);">用</font>**<font style="color:rgb(25, 27, 31);">多组参数去生成多组自注意力结果</font>**<font style="color:rgb(25, 27, 31);">。这样，每个单词的自注意力表示会更丰富一点。</font><font style="color:rgb(51, 51, 51);">模型可以从</font>**<font style="color:rgb(51, 51, 51);">不同的子空间学习</font>**<font style="color:rgb(51, 51, 51);">信息。</font>
+ **<font style="color:rgb(51, 51, 51);">目的</font>**<font style="color:rgb(51, 51, 51);">：这种设计使模型能够更好地理解语言的多种复杂关系，比如同义词和反义词关系、语法和语义关系等。</font>

#### **<font style="color:rgb(0, 0, 0);">3. 位置编码（Positional Encoding）</font>**
+ **<font style="color:rgb(51, 51, 51);">问题</font>**<font style="color:rgb(51, 51, 51);">：由于Transformer完全基于注意力机制，缺乏序列的位置信息。</font>
+ **<font style="color:rgb(51, 51, 51);">解决方案</font>**<font style="color:rgb(51, 51, 51);">：通过向输入序列的每个元素添加位置编码，模型能够利用这些信息来了解单词在句子中的位置关系。位置编码是与词嵌入相加的，以保留位置信息。</font>

#### **<font style="color:rgb(0, 0, 0);">4. 编码器-解码器架构</font>**
+ **<font style="color:rgb(51, 51, 51);">架构</font>**<font style="color:rgb(51, 51, 51);">：Transformer模型包含编码器和解码器两部分。编码器用于处理输入序列，解码器则基于编码器的输出和之前的解码器输出生成目标序列（解码器输出是串行的）。</font>
+ **<font style="color:rgb(51, 51, 51);">特点</font>**<font style="color:rgb(51, 51, 51);">：每个编码器和解码器层都包含多头注意力机制和前馈神经网络，通过残差连接和层归一化来优化训练过程。</font>

### 优缺点
优点：

1. 虽然Transformer最终也没有逃脱传统学习的套路，Transformer也只是一个全连接（或者是一维卷积）加Attention的结合体。但是其设计已经足够有创新，因为其抛弃了在NLP中最根本的RNN或者CNN并且取得了非常不错的效果，算法的设计非常精彩，值得每个深度学习的相关人员仔细研究和品位。
2. Transformer的设计最大的带来性能提升的关键是将任意两个单词的距离变成1，这对解决NLP中棘手的长期依赖问题是非常有效的。
3. Transformer不仅仅可以应用在NLP的机器翻译领域，甚至可以不局限于NLP领域，是非常有科研潜力的一个方向。
4. 算法的并行性非常好，符合目前的硬件（主要指GPU）环境。

缺点：

1. 粗暴的抛弃RNN和CNN虽然非常炫技，但是也使模型丧失了捕捉局部特征的能力，RNN + CNN + Transformer的结合可能会带来更好的效果。
2. Transformer失去的位置信息其实在NLP中非常重要，而论文中在特征向量中加入Position Embedding也只是一个权宜之计，并没有改变Transformer结构上的固有缺陷。
