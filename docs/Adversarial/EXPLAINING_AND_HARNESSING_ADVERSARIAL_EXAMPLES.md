<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$'],["\\(","\\)"]],
            displayMath: [
                ['$$', '$$'],
                ['\\[', '\\]']
                ],
            }
        });
    </script>
</head>

# EXPLAINING AND HARNESSING ADVERSARIAL EXAMPLES
[EXPLAINING AND HARNESSING ADVERSARIAL EXAMPLES](https://arxiv.org/abs/1412.6572)
## 介绍
当前机器学习已经被广泛应用在日常生活各个领域，但是Szegedy等人于2014年首先发现当前的机器学习模型包括神经网络等模型容易受到对抗样本(Adversarial Examples)的攻击。所谓对抗样本，即攻击者通过轻微地扰动正常样本产生对抗样本，在且保证该攻击不影响人眼的识别的情况下，达到误导分类器的目的。

在当前的研究中，对抗样本的原因产生的原因仍是一个谜。之前很多假设推测对抗样本的产生是因为深度神经网络的极度非线性，可能还结合了监督学习中正则化和模型均化不足等原因。但是本文的作者认为，这种非线性(Nonlinear)的推测解释没有必要，**高维空间的线性(Linear Behavior)足够产生对抗样本**(TODO 这句话的意思)。根据这个观点，作者设计了一种新的快速产生对抗样本的方法，并且使得对抗学习(Adversarial Training)更实用。这种对抗学习方法提供除了传统正则化方法(dropout, pre-training, model averaging等)外另外一种"正则化方法"。
## 相关工作
+ 对抗样本与原始样本的差别小到不能被人眼区分；
+ 即使对于不同结构的网络，或在不同数据子集上训练的网络，相同的对抗样本也总能造成错误分类；
+ 浅层模型如Shallow softmax regression也不能抵御对抗样本的攻击；
+ Adversarial Training能够提供正则化，但是其训练需要在内层循环中做大量的约束性优化。

因此，尽管神经网络能够得到很好的整体效果，但对于在数据分布中低概率出现的数据点，神经网络的表现可能就不好了。这表明神经网络并没有学习到完全正确的概念。
## 对抗样本的线性解释
论文介绍了对抗样本存在的线性解释。

在许多问题中，单个输入特征的精度受到限制。 例如，数字图像通常每个像素仅使用8位，因此它们会丢弃低于动态范围1/255的所有信息。

对抗样本的扰动本身不能太小
$$
\omega^T x'=\omega^T x+\omega^T \eta
$$
## FGSM
文章提出了一种 fast gradient sign method 用于生成对抗样本。
$$
\eta=\epsilon sign(\nabla_x J(\theta,x,y))
$$
## 对抗训练
$$
J'(\theta,x,y)=\alpha J(\theta,x,y)+(1-\alpha)J(\theta,x+\epsilon sign(\nabla_x J(\theta,x,y)),y)
$$

平衡准确性和对抗性
GAN里面的损失函数也有个类似的处理
##　不同类型的模型容量
为什么对抗样本的存在如此的违反直觉？
因为人类生活在三维空间中，对数百个维度中的小效果加起来创建大的效果并不习惯。

## 对抗样本泛化原因
对抗样本具有Transferability。具体来说，在一个特定模型上产生的对抗样本通常也容易被其他模型误分类，即使这些模型的结构不同或者模型在不同的训练集上训练。甚至，不同的模型对对抗样本误分类的结果相同

作者表明，非线性或者过拟合的假设不能解释上述的现象

## 对抗样本存在性

这一部分，作者通过实验及分析，反驳了其他两种对抗样本存在性的假设。

假设1：生成训练可以在训练过程中提供更多的限制，或者是的模型学习如何分辨"real"或者"fake"的数据，并且对"real"的数据更加自信。

文章表明，某些生成训练并不能达到假设的效果，但是不否认可能有其他形式的生成模型可以抵御攻击，但是确定的是生成训练的本身并不足够。

假设2：对抗样本存在于单个奇怪的模型(models with strange quirks)，因此多个模型的平均可以使得模型防御性更好。

模型融合对于对抗样本的防御能力非常有限。

## 总结
+ 对抗样本是模型过于线性的结果；

+ 对抗样本在不同模型间的泛化能力可以被解释为：对抗扰动与模型的权重向量高度对齐，不同模型在训练相同的任务时会学习到相似的功能；

+ 最重要的是扰动的方向，而不是空间中的特定点，因此对抗扰动在不同的样本中能够泛化；

+ 介绍了一系列用于生成对抗样本的快速方法；

+ 未能使用更简单的正则化方法重现此效果；

+ 易于优化的模型易受到干扰，比如线性模型；

+ 可对输入分布进行建模的模型不能抵御对抗样本；

+ 集成类方法不能对对抗扰动提供有限的抵御。
