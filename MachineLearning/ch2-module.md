# 模型描述

- $$m$$ 代表训练集中实例的数量
- $$ x$$ 代表特征/输入变量
- $$ y$$ 代表目标变量/输出变量
- $$(x,y)$$ 代表训练集中的实例
- $$(x^{(i)},y^{(i)})$$代表第 $$i$$ 个观察实例

$$h$$  代表学习算法的解决方案或函数也称为假设（**hypothesis**）。

# 代价函数

> 线性回归：函数去拟合数据分布，从而达到预测新数据的效果。
>
> 需要的知识是矩阵的计算，最小二乘法以及求偏微分。

主要公式
$$
Cost(\theta)=\frac{1}{2m}\sum^m_{i=1}(h_{\theta}(x^i)-y^i)^2
$$

$$
\theta_j = \theta_j - \alpha\frac{1}{m}\sum^m_{i=1}(h_{\theta}(x^i)-y^i)\frac{\partial h_{\theta}(x^i)}{\partial\theta_j}
$$

简单例子：$$( h_\theta(x) = \theta^{T}x = \theta_{0}+\theta_{1}x_{1} ) $$