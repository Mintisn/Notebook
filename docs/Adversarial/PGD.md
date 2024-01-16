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
# [Reliable Evaluation of Adversarial Robustness with an Ensemble of Diverse Parameter-free Attacks](https://arxiv.org/abs/2003.01690)

## Abstract

### PGD攻击的两个问题

**次优步长（Suboptimal Step Size）：** 在PGD算法中，每个迭代步骤都需要朝着损失函数的梯度方向前进，以生成对抗样本。步长是表示在梯度方向上前进的距离，通常会小于等于1，以确保不会跨过损失函数的局部极小值点。"次优步长"指的是在每个迭代步骤中，由于计算成本或其他因素，选择了一个不是最优的步长。这意味着在更新对抗样本时，可能没有在梯度方向上移动足够远，从而导致对抗样本的质量不如可能的最佳步长情况下生成的样本好。

**目标函数问题：** PGD的目标是生成一个对抗样本，使得模型在这个样本上的预测结果与原始样本的真实标签不同，即达到误分类的效果。目标函数问题指的是在PGD中所最小化的函数，这个函数是攻击者希望最小化的目标，它是损失函数（通常是交叉熵）和对抗项（使样本接近原始样本分布）的组合。攻击者的目标是找到一个对抗样本，使得这个函数的值最小化，从而达到成功的对抗攻击效果。

## Introduction

**PGD测试对抗鲁棒性也可能失败**:
+ 固定的步长
+ 广泛采用的交叉熵损失函数
+ 攻击之间缺乏多样性(白盒FAB攻击和黑盒Square攻击)

**补救措施**
+ Auto-PGD
+ 另一种替代的损失函数
+ AutoAttack

## Adversarial examples and PGD

对抗样本:

$$
\arg\max_{k=1,..K}g_{k}\neq c , d(x,z)\leq\epsilon
$$

PGD:
PGD的定义

## APGD

![APGD算法](https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20230825221227.png)

## AutoAttack

**全面的攻击策略：** AutoAttack 通过使用多种不同的对抗攻击方法来评估模型的鲁棒性。它不仅仅使用一种攻击方法，而是综合考虑了多个攻击方法，以提供更全面的评估。

**白盒和黑盒攻击：** AutoAttack 支持白盒攻击（攻击者知道模型架构和参数）和黑盒攻击（攻击者只能访问模型输出），从而模拟不同类型的攻击场景。

**多样的扰动范围：** AutoAttack 使用不同的扰动范围来对抗攻击，包括 L∞、L2 和 L1 范数。这样可以更全面地评估模型在不同范数下的鲁棒性。

**自动参数调整：** AutoAttack 提供了自动参数调整功能，可以根据模型的性质和数据集的特点自动选择最适合的攻击参数，以获得更具有挑战性的对抗性样本。

**评估指标：** AutoAttack 不仅仅考虑了单一的攻击成功率，还提供了多种评估指标，如 AutoAttack 性能、对抗样本的成功率、对抗样本的置信度等，以提供更全面的模型鲁棒性评估。