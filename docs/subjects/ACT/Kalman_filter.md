# 卡尔曼滤波

> 本文极大程度上参考了[BZARG的这篇文章](https://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/)，强烈推荐去读读原文。

> 如果你有现代控制理论的基础（了解状态空间表示），读这篇文章会相对容易。

假设我们已经获得了当前估计状态$x_k$，它是一个多元随机变量，因而应该有均值$\mathbf{\mu}$和协方差矩阵$\mathbf{\Sigma}$。

我们用均值来代表最优估计，且把协方差矩阵写为$\mathbf{P_k}$，即

$$
\begin{align}
    & \mathbf{\hat{x}_k} = \mathbf{\mu} \\
    & \mathbf{P_k} = \mathbf{\Sigma}
\end{align} 
$$

假设状态包括当前速度和位置两个标量，输入为加速度，那么应该有状态转移方程

$$
x_{k+1} = A x_k + Gu
$$

其中

$$
\begin{align}
    x_k &=
    \begin{bmatrix}
        p_k\\
        v_k\\
    \end{bmatrix}\\
    A &= 
    \begin{bmatrix}
    1 & \Delta t\\
    0 & 1
    \end{bmatrix} \\
    B &=
    \begin{bmatrix}
        \frac{1}{2}\Delta t^2 \\
        \Delta t
    \end{bmatrix} \\
    u &= a
\end{align}
$$

由于

$$
\begin{align}
    E(Ax) & = AE(x) \\
    \mathrm{cov}(Ax) & = A\mathrm{cov}(x)A^T
\end{align}
$$

有最优估计和协方差矩阵的递推公式

$$
\begin{align}
    \mathbf{\hat{x}_{k+1}} &= A\mathbf{\hat{x}_k} + Bu \\
    \mathbf{P_{k+1}} &= A\mathbf{P_k}A^T
\end{align}
$$

如果假设每一步状态转移时，环境都会向状态引入一个高斯白噪声，假设其与当前状态相互独立，由协方差的性质

$$
\mathrm{cov}(\sum_i X_i,\sum_j Y_j)=\sum_i \sum_j \mathrm{cov}(X_i,Y_j)
$$

可得，只需在上式后加一个噪声的协方差矩阵$\mathbf{Q}$

$$
\begin{align}
    \mathbf{P_{k+1}} = A\mathrm{P_k}A^T + \mathbf{Q}
\end{align}
$$

现在我们引入观测矩阵。就是说，现实中的物理量经过一个线性变换（也就是这个观测矩阵），变成了传感器读取到的数据。