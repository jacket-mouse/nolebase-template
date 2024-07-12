[TOC]

# 概率论

## 极大似然估计

> 概率是通过已知的条件，推测事件发生的可能性；似然则相反，是基于已经确定的结果反推产生这个结果的可能性。

$$
\theta：环境对应的参数 \\
x：事件发生的结果 \\
概率：P(x|\theta) \quad P是关于x的函数\\
似然：L(\theta|x) \quad L是关于\theta的函数
$$

极大（最大）似然估计：通过已知结果推测最大概率导致这些样本结果出现的模型参数。

## 2.4 Calculus

### 梯度

我们可以连结一个多元函数对其所有变量的偏导数，以得到该函数的*梯度*（gradient）向量。
具体而言，设函数$f:\mathbb{R}^n\rightarrow\mathbb{R}$的输入是一个$n$维向量$\mathbf{x}=[x_1,x_2,\ldots,x_n]^\top$，并且输出是一个标量。
函数$f(\mathbf{x})$相对于$\mathbf{x}$的梯度是一个包含$n$个偏导数的向量:

$$\nabla_{\mathbf{x}} f(\mathbf{x}) = \bigg[\frac{\partial f(\mathbf{x})}{\partial x_1}, \frac{\partial f(\mathbf{x})}{\partial x_2}, \ldots, \frac{\partial f(\mathbf{x})}{\partial x_n}\bigg]^\top,$$

其中$ \nabla_{\mathbf{x}} f(\mathbf{x}) $通常在没有歧义时被$\nabla f(\mathbf{x})$取代。

假设$\mathbf{x}$为$n$维向量，在微分多元函数时经常使用以下规则:

* 对于所有$\mathbf{A} \in \mathbb{R}^{m \times n}$，都有$\nabla_{\mathbf{x}} \mathbf{A} \mathbf{x} = \mathbf{A}^\top$
* 对于所有$\mathbf{A} \in \mathbb{R}^{n \times m}$，都有$\nabla_{\mathbf{x}} \mathbf{x}^\top \mathbf{A}  = \mathbf{A}$
* 对于所有$\mathbf{A} \in \mathbb{R}^{n \times n}$，都有$\nabla_{\mathbf{x}} \mathbf{x}^\top \mathbf{A} \mathbf{x}  = (\mathbf{A} + \mathbf{A}^\top)\mathbf{x}$
* $\nabla_{\mathbf{x}} \|\mathbf{x} \|^2 = \nabla_{\mathbf{x}} \mathbf{x}^\top \mathbf{x} = 2\mathbf{x}$

同样，对于任何矩阵$\mathbf{X}$，都有$\nabla_{\mathbf{X}} \|\mathbf{X} \|_F^2 = 2\mathbf{X}$​。
正如我们之后将看到的，梯度对于设计深度学习中的优化算法有很大用处。

> 关于梯度向量是行向量还是列向量？
>
> 都不是，行向量和列向量是从矩阵的角度来描述向量时才特有的，普通向量并没有必须放到矩阵中去，也没有所谓必须是行向量或者列向量的说法


### 练习

> 绘制函数$y = f(x) = x^3 - \frac{1}{x}$和其在$x = 1$​处切线的图像。

```python
import numpy as np
import matplotlib.pyplot as plt

def func(x):
    return x ** 3 - 1 / x
def numerical_lim(f,x):
    h = 1e-4
    return (f(x+h)-f(x))/h
def tangent_line(f, x):
    # d就是调用numerical_diff求得在x点点导数
    d = numerical_lim(f, x)
    # 这里直接y=kx+b求截，简单粗暴，y就是截距
    y = f(x) - d * x
    # 使用lambda匿名函数，t是形参，'：'后是要执行的函数表达式
    return lambda t: d * t + y

x = np.arange(0.1, 5, 0.1)
y = func(x)

plt.xlabel('x')
plt.ylabel('y')
# 把函数作为形参时i，传入实参函数时，只要函数名即可，不用()
tf = tangent_line(func,1)
# 因为tf返回的是lambda函数，所以要多调一次函数
y2 = tf(x)
plt.plot(x, y)
plt.plot(x, y2, linestyle='--')
plt.show()

```

> 求函数$f(\mathbf{x}) = 3x_1^2 + 5e^{x_2}$​的梯度。

$$
[6x_1,5e^{x_2}]
$$



> 函数$f(\mathbf{x}) = \|\mathbf{x}\|_2$​的梯度是什么？

$$
||x||_2 = \sqrt{\sum_{i=1}^{n}x_i^2} \\
=\sqrt{x_1^2 + x_2^2……+x_n^2} \\
D(||x||_2)= \frac{1}{2\sqrt{\sum_{i=1}^{n}x_i^2}}D(\sum_{i=1}^{n}x_i^2) \\
= \frac{x_i}{\sqrt{\sum_{i=1}^{n}x_i^2}} \\
\nabla_x||x||_2 = [\frac{x_1}{\sqrt{\sum_{i=1}^{n}x_i^2}}……\frac{x_n}{\sqrt{\sum_{i=1}^{n}x_i^2}}]
$$

> 尝试写出函数$u = f(x, y, z)$，其中$x = x(a, b)$，$y = y(a, b)$，$z = z(a, b)$的链式法则。

$$
\frac{\partial u}{\partial a} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial a} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial a} + \frac{\partial f}{\partial z} \frac{\partial z}{\partial a} \\
\frac{\partial u}{\partial b} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial b} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial b} + \frac{\partial f}{\partial z} \frac{\partial z}{\partial b} \\
$$

## 2.5 Automatic Differentiation

[[5分钟深度学习] #02 反向传播算法](https://www.bilibili.com/video/BV1yG411x7Cc/?spm_id_from=333.337.search-card.all.click&vd_source=519c4464a364b8611b8a226be3cda0f6)

在PyTorch中，`.requires_grad_(True)` 是一个用于设置张量（tensor）属性的方法，用于指示计算时是否需要计算梯度（gradient）。具体来说：

- `x.requires_grad_(True)` 表示将张量 `x` 的 `requires_grad` 属性设置为 `True`，这意味着当对 `x` 进行操作时，PyTorch会自动跟踪对 `x` 的计算，并且在计算过程中保留梯度信息，以便后续进行反向传播计算梯度。

通常情况下，我们会将需要参与模型训练的参数设置为 `requires_grad=True`，以便在优化过程中自动计算参数的梯度，从而更新参数。

举例说明：

```python
import torch

# 创建一个张量
x = torch.tensor([1.0, 2.0, 3.0], requires_grad=False)

# 设置 requires_grad=True，即需要计算梯度
x.requires_grad_(True)

# 进行一些计算
y = x.pow(2).sum()

# 反向传播，计算梯度
y.backward()

# 输出梯度
print(x.grad)  # 这里将会输出对应的梯度值
```

在这个例子中，我们将 `x` 的 `requires_grad` 属性设置为 `True`，然后进行了一些计算（计算了 `x` 的平方和 `y`），然后通过 `y.backward()` 反向传播计算了 `y` 对 `x` 的梯度。
![image-20240411201507888](https://1ees0n.oss-cn-qingdao.aliyuncs.com/OS/image-20240411201507888.png)

## 2.7 Documentation

为了知道模块中可以调用哪些函数和类：

- 查找模块的所有属性

```python
dir(torch.distributions)
```

通常可以忽略以“`__`”（双下划线）开始和结束的函数，它们是Python中的特殊对象， 或以单个“`_`”（单下划线）开始的函数，它们通常是内部函数。 根据剩余的函数名或属性名，我们可能会猜测这个模块提供了各种生成随机数的方法， 包括从均匀分布（`uniform`）、正态分布（`normal`）和多项分布（`multinomial`）中采样。

- 查找特定函数和类的用法

有关如何使用给定函数或类的更具体说明，可以调用`help`函数。 例如，我们来查看张量`ones`函数的用法。

```python
help(torch.ones)
```



# 3. 线性神经网络

## [3.1 线性回归](https://zh.d2l.ai/chapter_linear-networks/linear-regression.html)

给定一个数据集，我们的目标是寻找模型的权重$w$和偏置$b$​， 使得根据模型做出的预测大体符合数据里的真实价格。 输出的预测值由输入特征通过*线性模型*的仿射变换决定，仿射变换由所选权重和偏置确定。

![image-20240415151504433](https://1ees0n.oss-cn-qingdao.aliyuncs.com/OS/image-20240415151504433.png)

## 3.4 softmax回归

softmax回归是一个多类分类问题

![image-20240428101910628](https://1ees0n.oss-cn-qingdao.aliyuncs.com/OS/image-20240428101910628.png)

计算过程

![image-20240428103109002](https://1ees0n.oss-cn-qingdao.aliyuncs.com/OS/image-20240428103109002.png)

![image-20240428103203942](https://1ees0n.oss-cn-qingdao.aliyuncs.com/OS/image-20240428103203942.png)

所有输出o，都转化为y，且
$$
y_1+y_2+...+y_n = 1 \\
y_1,y_2,...,y_n \in [0,1]
$$
![image-20240428103528482](https://1ees0n.oss-cn-qingdao.aliyuncs.com/OS/image-20240428103528482.png)

- 独热编码

顾名思义，全连接层是“完全”连接的，可能有很多可学习的参数。 具体来说，对于任何具有𝑑个输入和𝑞个输出的全连接层， 参数开销为𝑂(𝑑𝑞)，这个数字在实践中可能高得令人望而却步。 幸运的是，将𝑑个输入转换为𝑞个输出的成本可以减少到𝑂(𝑑𝑞/𝑛)， 其中超参数𝑛可以由我们灵活指定，以在实际应用中平衡参数节约和模型有效性 ([Zhang *et al.*, 2021](https://zh.d2l.ai/chapter_references/zreferences.html#id195))。

## 损失函数

### l2 loss

$$
l(y,y') = \frac{1}{2}(y-y')^2
$$

### l1 loss

$$
l(y,y') = |y-y'|
$$

### Huber's Robust Loss

$$
l(y,y') =  
 \left\{ \begin{aligned}
            & |y-y'| - \frac{1}{2}  \quad if |y-y'| > 1\\ 
            & \frac{1}{2}(y-y')^2  \quad otherwise\\
            \end{aligned} 
 \right.
$$



## 书籍

[**机器学习、NLP面试中常考到的知识点和代码实现**](https://github.com/NLP-LOVE/ML-NLP)

[动手学深度学习](https://zh.d2l.ai/)

[最全西瓜书-周志华《机器学习》笔记](https://zhuanlan.zhihu.com/p/134089340)



## 论文

[颠覆传统！Transformer时序预测重大突破](https://mp.weixin.qq.com/s?__biz=MzkzOTY0NTMyNw==&mid=2247484236&idx=1&sn=e4dbbd9640c3dd6859e4472d4f0a0fa3&chksm=c2ec83acf59b0abab5ad2abc7ee7a9695a29fbe49bc1092ae3c508a7ebd73987afd087972028&mpshare=1&srcid=040103UKG3Z2vtYv04jCYtSk&sharer_shareinfo=1f092967f8efff9edb1867ba900c9c9d&sharer_shareinfo_first=1f092967f8efff9edb1867ba900c9c9d&from=singlemessage&scene=1&subscene=10000&clicktime=1712479943&enterid=1712479943&sessionid=0&ascene=1&fasttmpl_type=0&fasttmpl_fullversion=7146881-zh_CN-zip&fasttmpl_flag=0&realreporttime=1712479943238&devicetype=android-33&version=2800303d&nettype=WIFI&abtest_cookie=AAACAA%3D%3D&lang=zh_CN&countrycode=CN&exportkey=n_ChQIAhIQOaGT3wpVE8lXJRE9%2FXS90RLoAQIE97dBBAEAAAAAAE20MzVeRHkAAAAOpnltbLcz9gKNyK89dVj0Uyn1OTecrCjuAwvmjsyOfGdeA8XkeX1Z93ybHB1zCnZGm%2FH7LFjF2myPqesVVkco%2FnhX7MdZEDJtqAraEt%2FiQcmn%2BDDDUNl1tfVW1UlMY39zNikAHbAOpRe0QEyddY%2BfiFIPsiOidSY%2BfpMgPbirR1plpf2xnGAlvP%2FGHwPx0Pe%2FgzbWjk2KxkNqk69sOM0Wk72Srq%2F2PQZ2Z%2FufvbQOXvPL47hucDEEv4sKl%2F%2BCQYYx9Htg2lQD9vXds8nIB1p5uqc%3D&pass_ticket=QJa%2FjUpiVUbVodWSegV0ONI5nlrkzF7ORXVOquNIPbic1Q0pu%2Fw43vmhgnDyIXiian%2BlPKkB5YXhCjUdvD1bcg%3D%3D&wx_header=3)
