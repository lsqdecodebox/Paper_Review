# Paper_Review



### 关于类别不平衡问题：



#### focal loss

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





#### Dice Loss for Data-imbalanced NLP Tasks

来自香侬科技的一篇，还未开源，网友怀疑效果，不过值得试一试

https://arxiv.org/pdf/1911.02855.pdf

https://zhuanlan.zhihu.com/p/106802620

> At training time, each training instance contributes equally to the objective function, while at test time F1 score concerns more about positive examples.

这段话看了好一会儿，表达的其实是类别不均衡导致的问题，却以训练阶段和测试阶段的效果差异进行描述和表达。（以结果呈现，不以具体数学关系进行表述）

在词性标注、命名实体识别、阅读理解、释义识别（Paraphrase Identification） 任务上实验，这些任务也通常是data imbalance的。

引用了蛮多经典方法的论文，介绍他们的方法，但没有做评价，包括  data resample

Dice系数是一种集合相似度度量函数，通常用于计算两个样本的相似度，取值范围在[0,1]

![image-20200709150828147](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200709150828147.png)

![image-20200709151534098](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200709151534098.png)













#### TODO

BBPE

https://zhuanlan.zhihu.com/p/146114164



模型蒸馏

https://zhuanlan.zhihu.com/p/124215760

 



