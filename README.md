# Paper_Review

##### 符号表

@ 	20%熟悉度 （大体内容方向）

@@ 	  40%熟悉度 （摘要、标题、关键词）

@@@		60%熟悉度 （导言、结论以及图表）

@@@@ 		80%熟悉度 （全篇、数学公式、技术术语）

@@@@@		100%熟悉度（代码细节、应用）

------



#### 论文合集（TODO）

##### 2012年到2016年的高引TOP 100  机器学习

https://zhuanlan.zhihu.com/p/161460985



------

#### 关于类别不平衡问题：

##### focal loss

@@@

https://zhuanlan.zhihu.com/p/49981234

https://arxiv.org/pdf/1708.02002.pdf

背景：object detection的算法主要可以分为两大类：two-stage detector和one-stage detector

one-stage detector的准确率不如two-stage detector的原因，作者认为和样本的类别不均衡有关



![image-20200704230747690](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200704230747690.png)

目前针对类别不平衡问题，一般使用正负样本输入量0.5：0.5解决

focal loss提出的loss方案， 带有一个超参，需要调节； 是从量值的角度，主观地对分类的难易程度进行指数性的权衡处理（原文未细看，不晓得有什么详细的解释说明）。

从实验对比上看，它对比了OHEM（同样解决类别不平衡问题的一种方法），没有对比 设置正负样本比例的方法，效果待验证。

OHEM（online hard example mining），实现了在线学习的类别平衡方法

关于loss的思考： 目前loss是表达  梯度更新的力量 和 预测与目标值的差异 的关系，交叉熵是从信息量的角度进行把握这层关系，但我还无法将网络和信息量进行等同看待（待分析），因此这层关系能否再考察值得深入。





##### Dice Loss 

@@@       来自香侬科技的一篇，还未开源，网友怀疑效果，不过值得试一试

https://arxiv.org/pdf/1911.02855.pdf

https://zhuanlan.zhihu.com/p/106802620

> At training time, each training instance contributes equally to the objective function, while at test time F1 score concerns more about positive examples.

这段话看了好一会儿，表达的其实是类别不均衡导致的问题，却以训练阶段和测试阶段的效果差异进行描述和表达。（以结果呈现，不以具体数学关系进行表述）

在词性标注、命名实体识别、阅读理解、释义识别（Paraphrase Identification） 任务上实验，这些任务也通常是data imbalance的。

引用了蛮多经典方法的论文，介绍他们的方法，但没有做评价，包括  data resample

Dice系数是一种集合相似度度量函数，通常用于计算两个样本的相似度，取值范围在[0,1]

![image-20200709150828147](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200709150828147.png)

![image-20200709151534098](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200709151534098.png)





##### Long-tail learning via logit adjustment

@@  苏剑林推荐   互信息思想解决类别不平衡问题  https://kexue.fm/archives/7615







------

#### 神经网络架构问题：

##### Graph Structure of Neural Networks 

@@		何恺明团队解构神经网络

 https://arxiv.org/abs/2007.06559

解构为神经网络原子神经元的拓扑结构

 average path length measures the average shortest path distance between any pair of nodes

clustering coefficient measures the proportion of edges between the nodes within a given node’s neighborhood, divided by the number of edges that could possibly exist between them, averaged over all the nodes

两个参数下会有较优点。



##### 关于attention中的softmax运算复杂度 的优化

https://arxiv.org/abs/2006.16236  Transformers are RNNs: Fast Autoregressive Transformers with Linear Attention  @@@

[https://kexue.fm/archives/7546#%E4%B8%80%E8%88%AC%E7%9A%84%E5%AE%9A%E4%B9%89](https://kexue.fm/archives/7546#一般的定义)

如果直接去掉Softmax，问题是内积无法保证非负性

博文提出三种方法： 泰勒展开、QK分别softmax、核方法

论文中的linear attention 最后效果和原始的相当

苏介绍得好丰富详细呀，相关的reformer 、linformer

![img](C:\Users\Administrator\AppData\Local\YNote\data\qq6E9B3325D6DD15459B92C31E96574474\a0ab18d7d346433ea7ea98598246b7ef\clipboard.png)





##### The Next Generation of Neural Networks

@@  Hinton 著

https://dl.acm.org/doi/10.1145/3397271.3402425

他认为人工神经网络最重要的问题是想人类一样高效地使用无监督学习。

当前无监督学习有两种方式：1、如同bert一样的变分自编码。图像方面则网络太深了，需要处理图像细节，而非表征向量  2、训练两个网络...为了筛除无关的信息

详见视频

 过去20年，自编码器的困难：1、没有采用合适的神经元模型，relu比sigmoid或tanh更合适； 2、初始化权重没做好； 3、硬件算力不足

无监督对比学习，提出 对比损失  Contrastive Loss；建模样本间的局部关系、增强数据间表达的一致性，最新实现SimCLR

类似： Contrastive Loss https://zhuanlan.zhihu.com/p/116899404



##### RL算法发现算法

@  https://zhuanlan.zhihu.com/p/164518791

学习策略梯度（LPG）



#### 模型：



##### 博文：The Illustrated Transformer

@@   详细阐释了transformer，可以关注位置向量编码的源码

https://jalammar.github.io/illustrated-transformer/



##### Longformer 

@@@   https://arxiv.org/pdf/2004.05150.pdf

1、slide window的self attention

2、dilated slide window 

3、global(cls token) + slide window

测试 long document tasks ，WIkiHop、TriviaQA。

测试character level language modeling ，数据集enwiki8、text8 

（Language modeling is the task of predicting the next word or character in a document.https://nlpprogress.com/english/language_modeling.html）

在roberta上继续预训练的



##### Big Bird

@@@  random 2 + window 3 + global 2  解长序列问题，且证明了图灵完备性

https://arxiv.org/abs/2007.14062

在可计算性理论里，如果一系列操作数据的规则（如指令集、编程语言、细胞自动机）按照一定的顺序可以计算出结果，被称为图灵完备（turing complete） ；有能力执行条件跳转（if、while、goto语句）以及改变内存数据

编程语言都是图灵完备的

We show that BigBird is a universal approximator of sequence functions and is Turing complete, thereby preserving these properties of the quadratic, full attention model

Pérez et al. [73] showed that the full transformer is Turing Complete (i.e. can simulate a full Turing machine)



#### bert在语义相似度搜索的应用：

##### Sentence-BERT

@@@  

https://www.aclweb.org/anthology/D19-1410.pdf   https://www.codenong.com/cs106313990/   https://cloud.tencent.com/developer/article/1629591

孪生网络三种后接方式：

1、直接使用距离公式，cosine距离、欧式距离等得到两个文本的相似度

2、加MLP层，学习文本关系函数的映射，

3、 Triplet network

bert的句子输出向量三种方式：

1. cls token
2. avg pooling 
3. max pooling

使用预训练BERT和RoBERTa网络，并且只微调它来生成有用的句向量。这有效的减少了训练时间：SBERT微调小于20分钟，同时生成比同类句向量方法更好的向量。





##### SentPWNet

@@ 在语义相似度任务中（QQP、MRPC），对标了Sentence-BERT，结果还好

https://arxiv.org/pdf/2005.11347v1.pdf







#### 编码

BBPE

https://zhuanlan.zhihu.com/p/146114164



#### 模型蒸馏

https://zhuanlan.zhihu.com/p/124215760

 

#### 文本摘要

##### PEGASUS

@@ Pre-training with Extracted Gap-sentences for Abstractive Summarization

*https://arxiv.org/pdf/1912.08777.pdf*

新的自监督预训练目标：GSG(Gap Sentences Generation)

少量训练，优秀的结果





#### 文本对抗 & 模型有效性 & benchmark

##### Probing Neural Network Comprehension of Natural Language Arguments

@@@  https://arxiv.org/pdf/1907.07355.pdf

在Argument Reasoning Comprehension Task上分析模型做判断的线索

取逆否命题（颠倒数据） 77分降到53分



##### Keeping up with the BERTs: a review of the main NLP benchmarks

@@@   https://creatext.ai/blog-posts/nlp-benchmarking-superglue-xtreme

对NLP任务进行了分类：

单句任务、双句相似任务和推理任务（包括逻辑问题 (例如判断两个论点是否矛盾) ，即问答题和阅读理解题，）

GLUE的一个重要优点是，它提供了一个人类基准

结果表明，berts在推理判断型任务上会低于人类基准1-5百分点（逻辑、因果推理）

提出 SuperGLUE 、XTREME（multilingual）