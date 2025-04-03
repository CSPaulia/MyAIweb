# Cross Entropy

## Cross Entropy

$$
\text{H}_p(q) = \sum_x q(x) \log_2(\frac{1}{p(x)}) = - \sum_x q(x) \log_2(p(x))
$$

交叉熵为我们提供了一种表达两种概率分布的差异的方法。p和q的分布越不相同，p相对于q的交叉熵将越大于p的熵。

在实际计算中，

$$
\text{L} = \text{H}_p(q) = - \sum_x q(y|x) \log_2(p(y|x))
= - \frac{1}{N} \sum_x \sum_c y_{xc} \log_2(p(y_c|x))
$$

其中，$N$表示样本数量，$x$表示样本，$c$表示类别，$y_{xc}$表示类别为$c$时$x$的预测标签，只有$c$与真实标签的类别$\hat{c}$相同时，$y_{x\hat{c}} = 1$，即$q(y_{\hat{c}}|x)=1/N$，其余类别$y_{xc} = 0$，即$q(y_c|x)=0/N=0$。

举个例子，

| 预测（softmax归一化后） | 真实                          |
| :-------------------: | :---------------------------: |
| 0.1 0.2 0.7   | 0 0 1 |
| 0.3 0.4 0.3   | 0 1 0 |
| 0.1 0.2 0.7   | 1 0 0 |

计算损失函数值：

$$
\text{sample}~1~\text{Loss} = - (0 \times \log{0.1} + 0 \times \log{0.2} + 1 \times \log{0.7}) = 0.36
$$

$$
\text{sample}~2~\text{Loss} = - (0 \times \log{0.3} + 1 \times \log{0.4} + 0 \times \log{0.3}) = 0.92
$$

$$
\text{sample}~3~\text{Loss} = - (1 \times \log{0.1} + 0 \times \log{0.2} + 0 \times \log{0.7}) = 2.30
$$

$$
\text{L} = \frac{0.36+0.92+2.3}{3} = 1.19
$$


## KL Divergence

$$
\text{D}_{\text{KL}}(q \| p) = - \sum_i q(x) \log_2(p(x)) + \sum_x p(x) \log_2(p(x)) = \text{H}_p(q) - \text{H}(p)
$$

在交叉熵的基础上减去了p的熵，衡量了两个分布之间的距离。

在神经网络的训练当中，由于p往往是标签的分布，p的熵值是确定的。所以KL散度和交叉熵是等价的。但是由于交叉熵不惜要计算信息熵，计算更加简单，所以交叉熵使用更加广泛。

## Binary Cross Entropy

模型预测结果：

$$
P_\theta(y=1)=\theta ~~~~~~~ P_\theta(y=0)=1 - \theta
$$

合并上面两个式子，得到：

$$
p_\theta(y) = \theta^y(1-\theta)^{(1-y)}
$$

观测到这些数据点的对数似然为：

$$
l(\theta) = \log \prod^N_{i=1} p_\theta(y_i) = \log \prod^N_{i=1}\theta^y(1-\theta)^{(1-y)} = \sum_{i=1}^N [y_i\log \theta + (1-y_i)\log(1-\theta)]
$$

这个损失函数就是$y_i$与$\theta$的交叉熵$H_y(\theta)$。

