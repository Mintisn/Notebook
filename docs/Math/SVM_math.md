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

- 支持向量机原问题：

$$
\min_{\boldsymbol{w},b}f(\boldsymbol{w})=\frac{1}{2}\|\boldsymbol{w}\|_2^2,\quad\mathrm{ s.t. }\ y_i(\boldsymbol{w}^\top\boldsymbol{x}_i+b)\ge 1,\forall 1\le i\le m
$$

- 支持向量机对偶问题：

$$
\max_{\boldsymbol{\alpha}\ge 0}g(\boldsymbol{}\alpha) =-\frac{1}{2}\sum_{i=1}^m\sum_{j=1}^m \alpha_i\alpha_j y_iy_j\boldsymbol x_i^\top\boldsymbol{x}_j+\sum_{i=1}^m \alpha_i,\quad \mathrm{s.t.}\ \boldsymbol{y}^\top\boldsymbol\alpha=0
$$

你需要使用简单的数学公式回答以下问题：

## 具体要求
### Q1
1. 给出支持向量机最大间隔准则原问题的推导，解释分类超平面和支持超平面的含义。

样本点到超平面的几何间隔,与解析几何中的距离公式相似:
$$
\delta=y((\frac{w}{\|w\|})^T x+\frac{b}{\|w\|}) 
$$
这个间隔可以理解为对特征分类的确信度

现在确定一个分类器,对任意实数,当
$$
w^T x_i+b>=1,y_i=1\\
w^T x_i+b<=-1,y_i=-1
$$
对于这个分类器而言,有
$$
y_i(w^T x_i+b)>=1,(i=1,2,...,m)
$$
我们需要找到离超平面最近的数据点,然后让其具体超平面尽可能远,并求出对应的超平面(w,b)
$$
\arg\max_{w,b}(\min_i\frac{(y_i(w^T x_i+b))}{\|w\|})
\\=\arg\max_{w,b}(\frac{1}{\|w\|})
$$
故我们的目标是最大化$ \frac{1}{\|w\|} $,即最小化$ \|w\| $

考虑到其非负性,同时为了后续便于求导,我们最终将问题改写为
$$
\min_{\boldsymbol{w},b}f(\boldsymbol{w})=\frac{1}{2}\|\boldsymbol{w}\|_2^2,\quad\mathrm{ s.t. }\ y_i(\boldsymbol{w}^\top\boldsymbol{x}_i+b)\ge 1,\forall 1\le i\le m
$$

**分类超平面和支持超平面的含义**
+ 分类超平面：
分类超平面是SVM在二分类问题中得到的结果，它是一个 $n-1$ 维的超平面，将样本空间分成两个部分，每个部分包含一个类别的样本。在二维平面上，分类超平面是一条直线，而在高维空间中，它是一个平面。分类超平面的表达式可以写为：$w \cdot x + b = 0$，其中 $w$ 是权重向量，$b$ 是偏置项。分类规则是，样本点 $x$ 被分到类别 $1$，当且仅当 $w \cdot x + b > 0$，而被分到类别 $-1$，当且仅当 $w \cdot x + b < 0$。分类超平面是支持向量机中最终用于进行分类的决策边界。

+ 支持超平面：
支持超平面是在最大间隔准则下，离分类超平面最近的那些支持向量所在的超平面。支持超平面与分类超平面平行，它们之间的距离称为间隔。在二维平面上，支持超平面是一条直线，而在高维空间中，它是一个平面。支持向量是与支持超平面最近的样本点，它们是唯一决定分类超平面位置和方向的点。支持超平面的存在保证了分类超平面有最大的间隔，并且使得SVM具有较好的泛化性能。
### Q2
2. 给出对偶问题的推导，并回答问题：强对偶性在支持向量机中始终成立吗？


为了得到对偶问题，我们首先定义拉格朗日乘子 $\alpha_i \geq 0$，然后构建拉格朗日函数（Lagrangian）：

$$
L(w, b, \alpha) = \frac{\|w\|^2}{2} - \sum_{i=1}^{m} \alpha_i \left(y_i(w \cdot x_i + b) - 1\right)
$$

接下来，我们对拉格朗日函数分别对 $w$ 和 $b$ 求偏导数，并令其等于0，得到最优解的条件：
$$
 \begin{cases}
\frac{\partial L}{\partial w} = w - \sum_{i=1}^{m} \alpha_i y_i x_i = 0 \\
\frac{\partial L}{\partial b} = - \sum_{i=1}^{m} \alpha_i y_i = 0
 \end{cases}
$$
即
$$
\begin{cases}
 w = \sum_{i=1}^{m} \alpha_i y_i x_i\\
\sum_{i=1}^{m} \alpha_i y_i = 0
\end{cases}
$$

然后，将条件 $w = \sum_{i=1}^{m} \alpha_i y_i x_i$ 代入：
$$
L(b, \alpha) = \frac{\left\|\sum_{i=1}^{m} \alpha_i y_i x_i\right\|^2}{2} - \sum_{i=1}^{m} \alpha_i \left(y_i\left(\sum_{j=1}^{m} \alpha_j y_j x_j \cdot x_i + b\right) - 1\right)
$$
接下来，根据内积的性质展开第一项：
$$
\left\|\sum_{i=1}^{m} \alpha_i y_i x_i\right\|^2 = \sum_{i=1}^{m} \sum_{j=1}^{m} \alpha_i \alpha_j y_i y_j (x_i \cdot x_j)
$$
代入到拉格朗日函数中：
$$
L(b, \alpha) = \frac{1}{2}\sum_{i=1}^{m} \sum_{j=1}^{m} \alpha_i \alpha_j y_i y_j (x_i \cdot x_j) - \sum_{i=1}^{m} \alpha_i \left(y_i\left(\sum_{j=1}^{m} \alpha_j y_j x_j \cdot x_i + b\right) - 1\right)
$$
展开第二项并合并：
$$
L(b, \alpha)= \frac{1}{2}\sum_{i=1}^{m} \sum_{j=1}^{m} \alpha_i \alpha_j y_i y_j (x_i \cdot x_j) - \sum_{i=1}^{m} \sum_{j=1}^{m} \alpha_i \alpha_j y_i y_j (x_i \cdot x_j) - b \sum_{i=1}^{m} \alpha_i y_i + \sum_{i=1}^{m} \alpha_i
$$
简化后得到对偶问题的表达式：
$$
\max_{\boldsymbol{\alpha}\ge 0}g(\boldsymbol{}\alpha) =-\frac{1}{2}\sum_{i=1}^m\sum_{j=1}^m \alpha_i\alpha_j y_iy_j\boldsymbol x_i^\top\boldsymbol{x}_j+\sum_{i=1}^m \alpha_i,\quad \mathrm{s.t.}\ \boldsymbol{y}^\top\boldsymbol\alpha=0
$$
其中，$\alpha_i$ 是拉格朗日乘子，$x_i \cdot x_j$ 表示样本 $x_i$ 和 $x_j$ 之间的内积。

**强对偶性在支持向量机中始终成立吗？**

支持向量机具有强对偶性。强对偶性是指原始问题（Primal Problem）和对偶问题（Dual Problem）的最优解值相等，并且对偶问题的解也同时是原始问题的解。在支持向量机中，由于目标函数是凸函数，约束条件是线性的，且满足Slater条件，因此强对偶性始终成立。

这意味着我们可以通过求解对偶问题来得到原始问题的最优解，并且可以通过支持向量的拉格朗日乘子 $\alpha_i$ 来找到支持向量，并确定最优的分类超平面。由于对偶问题的解只涉及支持向量，而不需要所有样本，这使得SVM在处理大规模数据时具有较好的效率。

### Q3
3. 根据前面的结果推导**SVM的KKT条件**。


SVM的KKT条件是满足最优解的一组充要条件，包括原始问题的约束条件、对偶问题的约束条件和拉格朗日乘子的非负性。
KKT条件:
满足原始问题的约束条件:
$$
y_i(w \cdot x_i + b) - 1 \geq 0, \quad  i = 1, 2, \ldots, m
$$
满足对偶问题的约束条件:
$$
\alpha_i \geq 0, \quad i = 1, 2, \ldots, m$$
$$
\sum_{i=1}^{m} \alpha_i y_i = 0$$

满足强对偶性条件:
$$
\min\frac{\|w\|^2}{2} = \max_{\boldsymbol{\alpha}\ge 0}g(\boldsymbol{}\alpha) 
$$
满足拉格朗日乘子的互补松弛条件:
$$
\alpha_i \left(y_i(w \cdot x_i + b) - 1\right) = 0, \quad \text{for all } i = 1, 2, \ldots, m
$$
当满足上述条件时，我们可以得到SVM的最优解。

### Q4
4. 如果数据非线性可分怎么办？给出修改后的原问题和对偶问题。

线性不可分时，需要使用核技巧。可以通过使用核函数（Kernel function）将数据映射到高维特征空间，从而使其在高维空间中变得线性可分。通过引入核函数，可以将原始问题和对偶问题进行修改，以适应非线性可分的情况。

假设数据 $x_i$ 经过一个核函数 $\phi(x_i)$ 映射到高维特征空间，我们可以将原始问题修改为：

**修改后的原始问题**：
$$
\min\frac{\|w\|^2}{2}\quad\mathrm{ s.t.} \quad y_i(w \cdot \phi(x_i) + b) - 1 \geq 0, \quad \text{for all } i = 1, 2, \ldots, m$$

在修改后的原始问题中，我们的决策函数变为 $f(x) = w \cdot \phi(x) + b$。

引入核函数后，代入进去，对偶问题的形式为：

**修改后的对偶问题**：
$$
\max_{\boldsymbol{\alpha}\ge 0}g(\boldsymbol{}\alpha) = \sum_{i=1}^{m} \alpha_i - \frac{1}{2} \sum_{i=1}^{m} \sum_{j=1}^{m} \alpha_i \alpha_j y_i y_j K(x_i, x_j)\quad \mathrm{ s.t.} \sum_{i=1}^{m} \alpha_i y_i = 0$$

(其中，$K(x_i, x_j)$ 是核函数，它用来计算样本 $x_i$ 和 $x_j$ 在高维特征空间中的内积，而不是直接在原始特征空间中计算内积。)

### Q5
5. 在问题3.4的基础上，若**允许少量样本破坏约束**，应增加怎样的损失函数，请给出修改后的原问题和对偶问题。

如果允许少量破坏约束，就需要采用软间隔的方法。通过引入软间隔和松弛变量，软间隔支持向量机可以在允许少量样本破坏约束的情况下，更好地适应实际应用中可能存在的噪声和复杂情况。

我们引入了非负松弛变量 $\xi_i$，其中 $C$ 是一个超参数，用于平衡间隔的宽度和误分类的惩罚参数 $C$ 的选择会影响最终模型的泛化能力，较大的 $C$ 会使模型更加关注正确分类的样本，而较小的 $C$ 则允许更多的样本处于软间隔或错边状态。$\xi_i$ 表示第 $i$ 个样本的分类误差，即样本位于其正确的分类超平面的错边（margin）内，或者被错误地分类。

假设数据 $x_i$ 经过一个核函数 $\phi(x_i)$ 映射到高维特征空间，我们可以将原始问题修改为：

**修改后的原始问题**：
$$
\min\frac{\|w\|^2}{2}+ C \sum_{i=1}^{m} \xi_i\quad\mathrm{ s.t.} \quad y_i(w \cdot \phi(x_i) + b)  \geq 1 - \xi_i, \quad  i = 1, 2, \ldots, m
$$
对偶问题中，拉格朗日乘子 $\alpha_i$ 的范围在 $0$ 和 $C$ 之间，而不是只有 $0$ 和正无穷大。这样可以容许一部分样本的拉格朗日乘子在满足 $0 \leq \alpha_i \leq C$ 的条件下可以取到非零值，从而允许一些样本出现分类错误，但是在最优解中仍然受到约束。

**修改后的对偶问题**：
$$
\max_{\boldsymbol C\ge{\alpha}\ge 0}g(\boldsymbol{}\alpha) = \sum_{i=1}^{m} \alpha_i - \frac{1}{2} \sum_{i=1}^{m} \sum_{j=1}^{m} \alpha_i \alpha_j y_i y_j K(x_i, x_j)\quad \mathrm{ s.t.} \sum_{i=1}^{m} \alpha_i y_i = 0
$$


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