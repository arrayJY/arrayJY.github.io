---
title: 现代图形学入门(1)：变换
date: 2020-12-13 02:22:40
categories:
- 图形学
mathjax: true
---

### 变换矩阵

* 缩放矩阵(Scale Matrix)：横向缩放$s_x$，纵向缩放$s_y$

$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
s_x & 0 \\
0 & s_y
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
\\
$$

* 切变矩阵(Shear Matrix)：切变长度为$a$
  $$
  \begin{bmatrix}x' \\y'\end{bmatrix}=
  \begin{bmatrix}1 & a \\0 & 1\end{bmatrix}
  \begin{bmatrix}x \\y\end{bmatrix}\\
  $$
  
* 旋转矩阵(Rotate Matrix)：绕原点逆时针旋转角度$\theta$
  $$
  \begin{bmatrix}x' \\y'\end{bmatrix}
  =
  \begin{bmatrix}cos\theta & -sin\theta \\
  sin\theta & cos\theta \end{bmatrix}
  \begin{bmatrix} x \\y \end{bmatrix}\\
  $$
  
* 平移矩阵(Translation Matrix)：横向平移$t_x$，纵向平移$t_y$

$$
\begin{bmatrix}x' \\y' \end{bmatrix}
=
\begin{bmatrix}x \\ y\end{bmatrix}+
\begin{bmatrix} t_x \\ t_y\end{bmatrix}\\
$$

可以看到，除平移以外其他变换都可以写成一个矩阵乘另一个矩阵的形式。

### 齐次矩阵

为了使得平移和其他线性变换一样，可以表示为一个矩阵乘另一个矩阵，于是引入齐次矩阵。简而言之，齐次矩阵就是将原来的坐标矩阵扩展多一个维度。

首先将坐标扩展一个维度，如$(x,y)$变为$(x, y, \textbf{w})$。$w=1$时表示为点，$w=0$时表示为向量。
$$
二维点(x, y)的齐次矩阵：\begin{pmatrix} x & y &  \textbf{1} \end{pmatrix} \\
二维向量(x, y)的齐次矩阵：\begin{pmatrix} x & y & \textbf{0} \end{pmatrix}
$$
如果$w$**不为0或1**，要进行矩阵的归一化，即变形成$\begin{pmatrix} \frac{x}{w} & \frac{y}{w} & 1\end{pmatrix}$的形式。

这样的好处是可以轻松使用加减来进行点和向量的转换：

* 向量 - 向量 = 向量
* 向量 + 向量 = 向量
* 点 - 点 = 向量
* 点 + 点 = 两点连线中点（进行归一化后）

同样，变换矩阵也要加一个维度，此后线性变换矩阵和平移矩阵可以合并成一个矩阵，此后我们只用乘法就可以表示所有的变换。
$$
变换矩阵\begin{pmatrix} x' \\ y' \end{pmatrix} 
=
\begin{pmatrix} a & b \\ c & d \end{pmatrix}
\begin{pmatrix} x \\ y \end{pmatrix}
+
\begin{pmatrix} t_x \\ t_y \end{pmatrix}\\
齐次变换矩阵\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} 
=
\begin{pmatrix} a & b & t_x \\ c & d & t_y \\ 0 & 0 & 1 \end{pmatrix}
\begin{pmatrix} x \\ y \\ 1 \end{pmatrix}
$$

### 变换的顺序

一般先进行旋转再进行平移，因为旋转矩阵进行的是**绕原点**旋转，所以平移后旋转会使得图形在旋转时移动。

同理，如果相对一个顶点不在原点的图形进行绕顶点旋转，可以将图形先平移到顶点和原点重合，再进行旋转，最后平移回去。

多个变换结合在一起，其实就是多个变换矩阵相乘。矩阵不具有交换律，即$T_1 · T_2 \not= T_2·T_1$。多个矩阵的结合顺序是从右向左的，即
$$
T_n…T_3·T_2·T_1\begin{pmatrix}x \\ y \\ 1\end{pmatrix}
$$
的应用顺序是$T_1、T_2...T_n$。

### 三维坐标变换

和二维坐标类似，三维坐标$(x,y,z)$表示为$(x,y,z,\textbf{w})$，当$w=1$时表示三维空间的点，当$w=0$时表示为三维空间向量，如果$w$既不为0又不为1则要进行向量归一化。

而三维坐标的齐次变换矩阵可以写成：
$$
\begin{pmatrix}x' \\ y' \\ z' \\ 1 \end{pmatrix}
=
\begin{pmatrix}
a & b & c & t_x \\
d & e & f & t_y \\
g & h & i & t_z \\
0 & 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}x \\ y \\ z \\ 1 \end{pmatrix}
$$

* 缩放矩阵：$x$方向缩放$s_x$倍，$y$方向缩放$s_y$倍，$z$方向缩放$s_z$倍
  $$
  S(s_x, s_y, s_z) = 
  \begin{pmatrix}
  s_x & 0 & 0 & 0 \\
  0 & s_y & 0 & 0 \\
  0 & 0 & s_z & 0 \\
  0 & 0 & 0 & 1
  \end{pmatrix}
  $$

* 平移矩阵：平移$(t_x, t_y, t_z)$
  $$
  T(t_x, t_y, t_z) =
  \begin{pmatrix}
  0 & 0 & 0 & t_x \\
  0 & 0 & 0 & t_y \\
  0 & 0 & 0 & t_z \\
  0 & 0 & 0 & 1
  \end{pmatrix}
  $$

* 绕轴旋转矩阵：平面分别绕$x,y,z$轴旋转$\theta$角度
  $$
  R_x(\theta) =
  \begin{pmatrix}
  1 & 0 & 0 & 0 \\
  0 & cos\theta & -sin\theta & 0 \\
  0 & sin\theta & cos\theta & 0 \\
  0 & 0 & 0 & 1
  \end{pmatrix} \\
  R_y(\theta) =
  \begin{pmatrix}
  cos\theta & 0 & sin\theta & 0 \\
  0 & 1 & 0 & 0 \\
  -sin\theta & 0 & cos\theta & 0 \\
  0 & 0 & 0 & 1
  \end{pmatrix}\\
  R_z(\theta) =
  \begin{pmatrix}
  cos\theta & -sin\theta & 0 & 0 \\
  sin\theta & cos\theta & 0 & 0 \\
  0 & 0 & 1 & 0 \\
  0 & 0 & 0 & 1
  \end{pmatrix}
  $$
  

