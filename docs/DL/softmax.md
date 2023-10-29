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

# Softmax回归 & 交叉熵
## Softmax Summary
+ softmax 回归是一个多类分类模型
+ 使用softmax操作子得到每个类的预测置信度
+ 使用交叉熵来衡量预测和标号的区别

### 公式
$$\hat y =\frac{exp(O_i)}{\sum_k exp(O_k)}\tag{softmax公式}$$

### softmax和交叉熵损失
+ 交叉熵常用来衡量两个概率的区别:
$H(p,q)=\sum_i -p_i log(q_i)$
+ 将它作为损失
$ l(y,\hat y)=-\sum_i y_i log \hat y_i =-log \hat y_y$
+ 损失函数
$$ \partial l(y,\hat y)=softmax(o)_i -y_i $$

## LossFunction
### 从回归到多类分类 均方损失
$$ l(y,y') = \frac{1}{2} (y-y')^2 $$
### Huber's Robust Loss
优化的时候比较平滑 大的时候用绝对值
$$l(y,y')=
\begin{cases}
|y-y'|-\frac 1 2\,\, ,if >1\\
\frac 1 2 (y-y')^2\,\,,otherwise
\end{cases} $$