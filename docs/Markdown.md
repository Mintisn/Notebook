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

# Markdown
[史上最全Markdown公式、符号总结！！！](https://blog.csdn.net/weixin_42782150/article/details/104878759)
## 常用符号

空格=\&emsp

## 代码引用
```python

#!/usr/bin/env python3

print("Hello, World!");

```
## tex
$$加粗mathbf\{x\}= \mathbf{X}\\
偏导\backslash partial= \partial \\
积分 \backslash int=\int\\
求和 \backslash sum=\sum\\向量 \backslash overrightarrow\{AB\}=\overrightarrow{AB}\\
箭头 \backslash  vec x=\vec x\\ bar \backslash bar x=\bar x\\ 点\backslash dotx= \dot x\\
$$

### tex矩阵
$$
 \begin{pmatrix}
 0&1&2\\
 3&4&5\\
 6&7&8\\
 \end{pmatrix}
$$
```
 \begin{pmatrix}
 0&1&2\\
 3&4&5\\
 6&7&8\\
 \end{pmatrix}
```
## tex公式

$$
 {\textstyle \int f(x)\,dx}
$$
$$
\int\!\!\!\int_D f(x,y)dxdy
$$
```tex
$$
 {\textstyle \int f(x)\,dx}
$$
$$
\int\!\!\!\int_D f(x,y)dxdy
$$
```
### tex分段函数
$$
 f(x) = 
 \begin{cases}
 2x,\,\,x>0 \\
 3x,\,\,x\le0 \\
 \end{cases}
$$
```tex
 f(x) = 
 \begin{cases}
 2x,\,\,x>0 \\
 3x,\,\,x\le0 \\
 \end{cases}
```
## tex希腊字母表
$$
\backslash alpha=\alpha\\
\backslash beta=\beta\\
\backslash chi= \chi\\
\backslash Delta\backslash delta =\Delta\delta\\
\backslash epsilon=\epsilon\\
\backslash eta=\eta\\
\backslash Gamma \backslash gamma=\Gamma\gamma\\
\backslash iota=\iota\\
\backslash kappa\kappa\\
\backslash Lambda \backslash lambda=\Lambda\lambda\\
\backslash mu=\mu\\
\backslash nu=\nu\\
\backslash Omega\backslash  omega=\Omega\omega $$

# 基础语法
我是普通文字
~~我是删除线~~
*我是强调*
**我是加粗**

> 这是引用
>> 然后二级引用

可以看到,高亮语法是不支持的
==高亮==


