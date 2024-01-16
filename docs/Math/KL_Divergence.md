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
# KL 散度

KL散度用于计算某个分布保留的信息的多少[^1]

## 分布的熵

首先我们回顾一下概率分布的熵:

$$H=-\sum_{i=1}^Np(x_i)logp(x_i)$$

熵没有告诉我们可以实现这种压缩的最佳编码方案。信息的最佳编码是一个非常有趣的主题，但对于理解KL散度而言不是必需的。熵的关键在于，只要知道所需位数的理论下限，我们就可以准确地量化数据中有多少信息。现在我们可以对此进行量化，当我们将观察到的分布替换为参数化的近似值时，我们丢失了多少信息。



## 使用KL散度测量丢失的信息

Kullback-Leibler散度只是对我们的熵公式的略微修改。不仅仅是有我们的概率分布p，还有上近似分布q。然后，我们查看每个log值的差异：

$$D_{KL}(p||q)=\sum_{i=1}^{N}p(x_i)(logp(x_i)-logq(x_i))$$



## 参考文献

[^1]:  [Kullback-Leibler(KL)散度介绍 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/100676922)
[^2]: [交叉熵和KL散度有什么区别？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/292434104)

[]
