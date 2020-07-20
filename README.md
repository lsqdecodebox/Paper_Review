# Paper_Review

##### 符号表

@ 	20%熟悉度 （大体内容方向）

@@ 	  40%熟悉度 （摘要、标题、关键词）

@@@		60%熟悉度 （导言、结论以及图表）

@@@@ 		80%熟悉度 （全篇、数学公式、技术术语）

@@@@@		100%熟悉度（代码细节、应用）

------







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





##### Dice Loss for Data-imbalanced NLP Tasks

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



#### 编码

BBPE

https://zhuanlan.zhihu.com/p/146114164



#### 模型蒸馏

https://zhuanlan.zhihu.com/p/124215760

 

#### 文本摘要

##### PEGASUS: Pre-training with Extracted Gap-sentences for Abstractive Summarization

@@

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