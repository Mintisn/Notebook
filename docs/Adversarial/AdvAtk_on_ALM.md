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
# Universal and Transferable Adversarial Attacks on Aligned Language Models

|                            paper                             |                             url                              |                            author                            | date        |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | ----------- |
| Universal and Transferable Adversarial Attacks on Aligned Language Models | [2307.15043.pdf (arxiv.org)](https://arxiv.org/pdf/2307.15043.pdf) | [Andy Zou](https://arxiv.org/search/cs?searchtype=author&query=Zou,+A), [Zifan Wang](https://arxiv.org/search/cs?searchtype=author&query=Wang,+Z), [J. Zico Kolter](https://arxiv.org/search/cs?searchtype=author&query=Kolter,+J+Z), [Matt Fredrikson](https://arxiv.org/search/cs?searchtype=author&query=Fredrikson,+M) | 27 Jul 2023 |

[llm-attacks/llm-attacks: Universal and Transferable Attacks on Aligned Language Models (github.com)](https://github.com/llm-attacks/llm-attacks)

## Abstract

+ recent work has focused on aligning these models in an attempt to prevent undesirable generation
+ **automatic** adversarial prompt generation have also achieved limited success
+ finds a suffix that aims to maximize the probability that the model produces an affirmative response
+ greedy and gradient-based search techniques

## 1     Introduction



+ there exist a number of published “`jailbreaks` ,” carefully engineered prompts that result in aligned LLMs generating clearly objectionable content [Wei et al., 2023]. 
+ **Disadvantage**:`jailbreaks` are typically crafted through human ingenuity rather than automated methods, requiring **substantial manual effort**
+ **challenges** :  `automatic prompt-tuning` unable to generate reliable attacks through automatic search methods ( This owes largely to the fact that, unlike image models, LLMs operate on **discrete** token inputs, which both substantially **limits the effective input dimensionality**, and seems to induce a computationally difficult search)
  + 图像模型使用**连续**像素值，可以通过微小的扰动来创建对抗性示例。LLMs使用**离散**标记，这些标记不能通过微小的扰动来改变，而只能用其他标记替换它们。
  + 图像模型具有**高维**输入空间，这意味着有许多可能的方法来扰动图像。LLMs具有**低维**输入空间，这意味着更少的可能性来改变文本。
  + 图像模型具有**平滑**的损失景观，这意味着损失函数随着输入的变化而逐渐变化。LLMs具有**不平滑**的损失景观，这意味着损失函数可以随着输入的变化而突然变化。
  + 这些差异使得使用基于梯度的方法更容易找到图像模型的对抗性示例，但使用相同方法更难找到LLMs的对抗性示例。LLMs需要更复杂的离散优化方法来找到有效的攻击。
+ **New attacks** :appends a adversarial suffix to the query that attempts to induce negative behavior (three key elements)
  +  **Initial affirmative responses.** 这里提到的理念和LLM Self Defense中大致相同,就是一个affirmative的开头容易让模型进入状态
  +  **Combined greedy and gradient-based discrete optimization.** similar to the `AutoPrompt` approach, but with the (we find, practically quite important) difference that we search over all possible tokens to replace at each step, rather than just a single one.
  +  **Robust multi-prompt and multi-model attacks** 也就是说, 去找同时能满足多个提问和模型的adv suffix



> [通过对抗性后缀攻击大型语言模型 - LLM Safety论文精读(三) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/662098517)

## 2    A Universal Attack on LLMs

对于一个LLM来说,实际上的输入并不只是 user 的输入, 同时还包括一段system prompt, 因此用户本身能控制的prompt其实很少. 

![20231108200633](https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231108200633.png)

### 2.1    Formalizing the adversarial objective

首先把LLM简化为一个序列模型,那么通过序列$x_{1:n}$预测到的下一个token的概率为:
$$
p(x_{n+1}\vert x_{1:n})
$$
此外有:
$$
p(x_{n+1:n+H}\vert x_{1:n})=\prod_{i=1}^{H}p(x_{n+i}\vert x_{1:n+i-1})
$$
而我们攻击的目标则是使得LLM生成一些关键序列($x_{n+1:n+H}^{\star}$)

那么相应的对抗损失则是:
$$
\mathcal{L}(x_{n+1})=-\log p(x_{n+1:n+H}^{\star}\vert x_{1:n})
$$

所以,寻找adversarial suffix的过程就变成了:

$$
minimize_{x_{\mathcal{I}\in\{1,2,..V\}^{\vert x \vert}} \mathcal{L}(x_{n+1})}
$$



### 2.2    Greedy Coordinate Gradient-based Search

![20231108210156](https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231108210156.png)

the straightforward approach to optimize a discrete of inputs:**simple extension of the AutoPrompt method**

**comprehension**

+ 首先找到对应$suffix_i$ 下梯度最大的k个token
+ 然后每次随机替换其中的一个token,批量操作得到B个$x_i$,每次选择其中表现最好的一个,更新$x_i$
+ 重复上面操作n次,得到了一个经过T次迭代的$x_i$

**hesitation**

+ 一开始的候选k个token是具体怎么得到的?

+ suffix是否一开始设定了长度?

**GCG is quite similar to the AutoPrompt**

> [[2010.15980\] AutoPrompt: Eliciting Knowledge from Language Models with Automatically Generated Prompts (arxiv.org)](https://arxiv.org/abs/2010.15980)

### 2.3 Universal Multi-prompt and Multi-model attacks


![20231108223017](https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231108223017.png)

**comprehension**

+ 这个算法对"universal"的实现是递增的,即等到p对其中某个propmt work后再针对下一个prompt优化
+ 这种递增的算法yields better results than attempting to optimize all prompts at once from the start.

## 3  Experimental Results: Direct and Transfer Attacks

TODO

![20231108230709](https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231108230709.png)



![20231108231650](https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231108231650.png)

## 5 Conclusion and Future Work

**conclusion**

+ 这个论文的方法是 a collection of techniques that had been previously considered
+ 但是这种方法从应用的角度来说很不错了

**future work**

+ 目前的攻击方法的提出最终可能使得大模型更加强大,甚至于目前迅速发展的大模型可能很快会解决了此类攻击

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        

