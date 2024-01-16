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

# 多层感知机
## 感知机
### loss function
$$\partial (y,\mathbf{X},\mathbf{W})= max(0,-y<W,X>) $$
### 收敛定理
+ 数据在半径内

+ 余量 $\rho$分类两类
$$
  
  y(X^TW+b)>=\rho,对于||W||^2+b^2<=1 

$$

+ 在$\frac{r^2+1}{\rho^2} $收敛
### [XOR问题](https://www.jianshu.com/p/853ebc9e69f6 "感知机不能解决异或(XOR)问题") (Minsky & Papert ,1969)  
+ 不能拟合XOR问题,只能产生线性分割面
于是有了多层感知机
## 多层感知机
### 单隐藏层
+ 输出$x\in R^n$
+ 隐藏层 $W_1\in R^{m*n},b_1\in R^m $
+ 输出层$W_2\in R^{m},b_2\in R $
    + $\mathbf{h}=\sigma(W_1x+b_1)$($\sigma 为激活函数$)
    + $o=W_2^Th+b_2$
+ 激活函数
    + sigmod激活函数
    + Tanh激活函数
    + ReLU激活函数(算得快)
### 多类分类 
+ 输出$x\in R^n$
+ 隐藏层 $W_1\in R^{m*n},b_1\in R^m $
+ 输出层 $W_2\in R^{m*k},b_2\in R^k $
    + $\mathbf{h}=\sigma(W_1x+b_1)$($\sigma 为激活函数,h表示隐藏层 $)
    + $o=W_2^Th+b_2$
    + $y=softmax(o)$
    可以有多个隐藏层h
+ 超参数: 隐藏层数,每层隐藏层的大小
    + 逐层压缩,避免损失太多信息

