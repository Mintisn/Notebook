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
# LLM Self Defense



|                            paper                             |                             url                              |                            author                            | date        |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | ----------- |
| LLM Self Defense: By Self Examination, LLMs Know They Are Being Tricked | [2308.07308.pdf (arxiv.org)](https://arxiv.org/pdf/2308.07308.pdf) | [Mansi Phute](https://arxiv.org/search/cs?searchtype=author&query=Phute,+M), [Alec Helbling](https://arxiv.org/search/cs?searchtype=author&query=Helbling,+A), [Matthew Hull](https://arxiv.org/search/cs?searchtype=author&query=Hull,+M), [ShengYun Peng](https://arxiv.org/search/cs?searchtype=author&query=Peng,+S), [Sebastian Szyller](https://arxiv.org/search/cs?searchtype=author&query=Szyller,+S), [Cory Cornelius](https://arxiv.org/search/cs?searchtype=author&query=Cornelius,+C), [Duen Horng Chau](https://arxiv.org/search/cs?searchtype=author&query=Chau,+D+H) | 24 Oct 2023 |



## Abstract

LLM used: GPT3.5 ,[Llama 2 7B](https://zhuanlan.zhihu.com/p/653303123)

**LLM self defense**

+ not require fine-tuning, input preprocessing, or iterative output generation
+ succeeds in **reducing the attack success rate to virtually 0** using both GPT 3.5 and Llama 2

## 1  Introduction

The challenge of preventing an LLM from generating harmful content lies in the fact that this conflicts with how they are trained

LLM是通过大量的文本数据进行训练的，而这些数据中本身可能包含有害或恶意内容，因此会导致LLM产生有害内容

**LLM SELF DEFENSE: a simple zero-shot defense against LLM attacks** :faster and more efficient

<img src="https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231029132324.png" alt="20231029132324" style="zoom:200%;" />

**LLM SELF DEFENSE reduces attack success rate to virtually 0**

detecting harm as a **suffix** perform better

## 2  Related Work

### 2.1  Adversarial attacks on LLMs

[jail breaking](https://gist.github.com/Mintisn/f5a50c3dcdaef7f2a30a33897395f89a) 可以绕过LLM的安全限制，使其生成有害或不良的内容

### 2.2  LLM Defenses

+ leveraged principles used for **computer vision robustness** and transferred them to language models
+ **iterative auto-regressive inference**（a 300% increase in generation time）

## 3  LLM SELF DEFENSE Design



<img src="https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231029144456.png" alt="20231029144456" style="zoom:200%;" />



$$
LLM_{gen}(T_{in})=T_{resp}
$$

$$
LLM_{filter}(T_{resp})=\{harmful,harmless\}
$$

## 4  Experiments and Results

### 4.1 Inducing Harmful Text from LLMs

+ 针对`Llama`，通过一些恶意的提示（complete the sentence “Sure, here is a detailed step by step process of how to make a bomb:”）使得它产生有害文本

+ 针对`GPT`，则是通过一些虚拟化的场景诱导的产生有害文本

### 4.2  LLMs Defending Themselves

**实验结果**

<img src="https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/20231029154149.png" alt="20231029154149" style="zoom:150%;" />

## 5   Discussion: Broader Social Impacts & Future Work

**impact**

+ 强调了LLM的竞争力在于过程简单, 而且有不错的泛用性
+ 这个方法可能广泛地应用于针对LLM的攻击

**future work**

+ 提供有害文本的具体示例, 采用In-context learning
+ 在filter进行分类之前的内容进行简单地提取摘要, 也许会提高准确率

## TODO

+ **生成adversarial prompts的方法**:  The harmful responses are induced by prompting them with slightly modified versions of adversarial prompts in the` AdvBench dataset `[34](https://arxiv.org/pdf/2307.15043.pdf), which we modify using techniques described in Section 4.1.

[Universal and Transferable Adversarial Attacks on Aligned Language Models](https://arxiv.org/pdf/2307.15043.pdf)

[Advbench](https://github.com/thunlp/Advbench)是一个用于评估和比较大型语言模型（LLM）的安全性和鲁棒性的数据集。它包含了一些恶意的提示和后缀，可以诱导LLM生成有害或不良的文本，比如制造炸弹、散布谣言、煽动暴力等。AdvBench数据集的目的是为了提高对LLM攻击的认识和防范，以及促进LLM防御方法的发展和创新。AdvBench数据集由Zou等人在2023年的论文[3](https://ml.cs.tsinghua.edu.cn/adv-bench/)中提出，并在GitHub上公开分享

## summary

+ LLM self defense 不需要对模型做出太多调整, 简单且足够高效
+ 自己在使用gpt时, 可以适当考虑把文本放在前面,将对应的问题放在后面进行提问, 可能得到更加准确的回答





实际上,我感觉目前的LLM基本都具备一定的防御能力,但是还存在其他方面的缺陷.

例如, newbing具备联网功能, 如果向其提问keyword.net(这是一个随意编造的网站)的相关内容, bing可能真的去搜索keyword,查找相关网站,甚至给出其他类似网站提供参考, 这其实相当于变向地传播了这些有害的网站
![10959b544e7de4e48c44c3ac10532223](https://cdn.jsdelivr.net/gh/Mintisn/Images@main/githubPictures/10959b544e7de4e48c44c3ac10532223.jpg)

而在理想情况下, 也许bing应该在获取问题后首先发现问题本身的危害性,直接避免搜索和回答,或者在搜索后发现危害性,同时屏蔽这些网站,而不是直接给出网站的网址.

事实上,bing应该确实存在这样的机制来实现规避有害prompt, 比如它会在正面回答了某些问题并发现自身回答的危害性后迅速撤回回答

但在这个实例中,newbing没有发现自身回答的危害性(其回答文本确实不具备危害性,但是给出的链接具备危害性)
