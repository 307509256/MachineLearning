# 函数家族

---

## 神经元模型

从最简单的说起：线性神经元


$$
 { y }=b +\sum_i { x}_{ i }{ w }_{ i }
$$


McCulloch-Pitts接着提出了二值的，必须达到阈值才发送一定量的冲激函数。

之后的Rectified Linear Neurons\(Linear threshold neuron\)超出阈值的部分仍是线性的。

Simoid neurons可以说是用连续函数版的二值，通常使用Logistic函数，这样一来求导方便。

接下来又有了Stochastic的处理，输出（0~1）作为产生冲激（1）的概率

### 激活函数（Activation Function）

为了让神经网络能够学习复杂的决策边界（decision boundary），我们在其一些层应用一个非线性激活函数。最常用的函数包括  sigmoid、tanh、ReLU（Rectified Linear Unit 线性修正单元） 以及这些函数的变体。

* **motivation**: to compose _simple transformations_ in order to obtain 
  _highly non-linear_ ones
* (MLPs compose affine transformations and element-wise non-linearities)
* hyperbolic tangent activation functions:

  $$
  { h }^{ k }=tanh({ b }^{ k }+{ W }^{ k }{ h }^{ k-1 })
  $$
  ![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/Sinh_cosh_tanh.svg/256px-Sinh_cosh_tanh.svg.png)

* the input of the neural net: $${ h }^{ 0 }=x$$
* theoutputofthe k-th hidden layer: $${ h }^{ k }$$

* affine transformation $$a = b+Wx$$, elementwise


  $$
  h=\phi (a)⇔{ h }_{ i }=\phi ({ a }_{ i })=\phi ({ b }_{ i }+{ W }_{ i,: }x)
  $$

* non-linear neural network activation functions:

  ###### Rectifier or rectified linear unit \(ReLU\) or positive part

  ###### Hyperbolic tangent

  ###### Sigmoid

  ###### Softmax

  ###### Radial basis function or RBF

  ###### Softplus

  ###### Hard tanh

  ###### Absolute value rectification

  ###### Maxout

* the structure (also called architecture) of the family of input-output functions can be varied in many ways: 
  _convolutional networks_, 
  _recurrent networks_

### Softmax

Softmax 函数通常被用于将原始分数（raw score）的矢量转换成用于分类的神经网络的输出层上的类概率（class probability）。它通过对归一化常数（normalization constant）进行指数化和相除运算而对分数进行规范化。如果我们正在处理大量的类，例如机器翻译中的大量词汇，计算归一化常数是很昂贵的。有许多种可以让计算更高效的替代选择，包括分层 Softmax（Hierarchical Softmax）或使用基于取样的损失函数，如 NCE。

* designed for the purpose of specifying **multinoulli distributions**:

  $$
  p=softmax(a)\Longleftrightarrow { p }_{ i }=\frac { { e }^{ { a }_{ i } } }{ \sum { _{ j }^{  }{ { e }^{ { a }_{ j } } } }  }
  $$

* consider the gradient with respect to the scores $$a$$.

  $$
  \frac { ∂ }{ ∂{ a }_{ k } } { L }_{ NLL }(p,y)=\frac { ∂ }{ ∂{ a }_{ k } } (−log{ p }_{ y })=\frac { ∂ }{ ∂{ a }_{ k } } ({ −a }_{ y }+log\sum _{ j }^{  }{ { e }^{ { a }_{ j } } } )\\ ={ −1 }_{ y=k }+\frac { { e }^{ { a }_{ k } } }{ \sum _{ j }^{  }{ { e }^{ { a }_{ j } } }  } ={ p }_{ k }-{1}_{y=k}
  $$


  or

  $$
  \frac { ∂ }{ ∂{ a }_{ k } } { L }_{ NLL }(p,y)=(p-{e}_{y})
  $$


在实现softmax函数的时候，为了防溢出有一个小trick：减去最大值。softmax函数如下：
$$
f(x)_i=\frac{e^{x_i}}{\sum_{j=1}^ne^{x_j}},j=1,2,\dots,n
$$

通常情况下，计算softmax函数值不会出现什么问题，如下图所示：

![](/assets/softmax.jpg)

但是，当某些情况发生时，计算函数值就出问题了：

 - $c$极其大，导致分子计算$e^c$时上溢出
 - $c$ 为负数，且$|c|$很大，此时分母是一个极小的正数，有可能四舍五入为0，导致下溢出

解决方法是，令$M=max(x_i),i=1,2,⋯,n$，即$ M$ 为所有 $x_i$ 中最大的值，那么我们只需要把算 $f(x)_i$的值，改为计算$f(x_i−M)$的值，就可以解决上溢出、下溢出的问题了，并且，计算结果理论上仍然和 $f(x)_i$保持一致。

在实现时也犯了一个低级错误：激活函数一开始弄错成了$1／1-e^{-x}$，发现交叉熵是26上下，忽略了全蒙（weight、bias全零）情况是$\log(250)\approx 5$。

### ReLU

即线性修正单元（Rectified Linear Unit）。ReLU 常在深度神经网络中被用作激活函数。它们的定义是 $$f(x) = \max(0, x)$$ 。ReLU 相对于 tanh 等函数的优势包括它们往往很稀疏（它们的活化可以很容易设置为 0），而且它们受到梯度消失问题的影响也更小。ReLU 主要被用在卷积神经网络中用作激活函数。ReLU 存在几种变体，如Leaky ReLUs、Parametric ReLU (PReLU) 或更为流畅的 softplus近似。

论文：深入研究修正器（Rectifiers）：在 ImageNet 分类上超越人类水平的性能（Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification）  
论文：修正非线性改进神经网络声学模型（Rectifier Nonlinearities Improve Neural Network Acoustic Models ）  
论文：线性修正单元改进受限玻尔兹曼机（Rectified Linear Units Improve Restricted Boltzmann Machines  ）

## Cost Functions

* a good choice for the criterion is maximum likelihood regularized with dropout, possibly also with weight decay.

### 分类交叉熵损失（Categorical Cross-Entropy Loss）

分类交叉熵损失也被称为负对数似然（negative log likelihood）。这是一种用于解决分类问题的流行的损失函数，可用于测量两种概率分布（通常是真实标签和预测标签）之间的相似性。它可用 $$L = -\sum(y * \log(y_{prediction}))$$ 表示，其中 y 是真实标签的概率分布（通常是一个one-hot vector），$$y_{prediction} $$是预测标签的概率分布，通常来自于一个 softmax。

### 负对数似然（NLL：Negative Log Likelihood）

参见分类交叉熵损失（Categorical Cross-Entropy Loss）。

#### Optimization Procedure

* a good choice for the optimization algorithm for a feed-forward network is usually stochastic gradient descent with momentum.

#### 6.3.2 Loss Function and Conditional Log-Likelihood

* In the 80’s and 90’s the most commonly used loss function was the squared error

  $$
  L({ f }_{ θ }(x),y)={ ||fθ(x)−y|| }^{ 2 }
  $$

* if f is unrestricted \(non- parametric\),


  $$
  f(x) = E[y | x = x]
  $$

* Replacing the squared error by an absolute value makes the neural network try to estimate not the conditional expectation but the conditional median

* **交叉熵（cross entropy）目标函数 **: when y is a discrete label, i.e., for classification problems, other loss functions such as the Bernoulli negative log-likelihood4 have been found to be more appropriate than the squared error. \($$y∈{ \left\{ 0,1 \right\}  }$$\)


$$
L({ f }_{ θ }(x),y)=−ylog{ f }_{ θ }(x)−(1−y)log(1−{ f }_{ θ }(x))
$$


* $${f}_{\theta}(x)$$ to be strictly between 0 to 1: use the sigmoid as non-linearity for the output layer\(matches well with the binomial negative log-likelihood cost function\)

##### Learning a Conditional Probability Model

* loss function as corresponding to a conditional log-likelihood, i.e., the negative log-likelihood \(NLL\) cost function

  $$
  { L }_{ NLL }({ f }_{ \theta  }(x),y)=−logP(y=y|x=x;θ)
  $$

* example\) if y is a continuous random variable and we assume that, given x, it has a Gaussian distribution with mean ${f}\_{θ}$\(x\) and variance ${\sigma}^{2}$

  $$
  −logP(y|x;θ)=\frac { 1 }{ 2 } { ({ f }_{ \theta  }(x)−y) }^{ 1 }/{ σ }^{ 2 }+log(2π{ σ }^{ 2 })
  $$

* minimizing this negative log-likelihood is therefore equivalent to minimizing the squared error loss.

* for discrete variables, the binomial negative log-likelihood cost func- tion corresponds to the conditional log-likelihood associated with the Bernoulli distribution \(also known as cross entropy\) with probability $p = {f}\_{θ}\(x\)$ of generating y = 1 given x =$$ x$$


  $$
  {L}_{NLL}=−logP(y|x;θ)={−1}_{y=1}{logp−1}_{y=0}log(1−p)\\ =−ylog{f}_{θ}(x)−(1−y)log(1−{f}_{θ}(x))
  $$



