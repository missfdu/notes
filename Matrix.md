---
title: Matrix
date: 2020-12-02 15:25:29
tags: [Math,Matlab]
categories: 记录
math: true
---

## Matlab基础

### 矩阵的生成

**直接法**

```matlab
matrix = [1, 2, 3; 4, 5, 6; 7, 8, 9]
```

**冒号生成一维矩阵**

```matlab
% 矩阵 = 开始数字 ：步长 ：截止数字
matrix = 1 : 2 : 10
```

**函数生成**

`linspace()`

```matlab
% 矩阵 = linspace(起始位置，终止位置，生成个数)
matrix = linspace(1, 5, 5)
```

`eye()`单位矩阵

```matlab
% 矩阵 = eye(n) n 为须要生成的单位矩阵的阶数
matrix = eye(3)
```

`zeros()` 全零矩阵

```matlab
% 矩阵 = zeros(行数，列数)
matrix = zeros(2, 2)
```

`ones()`全一矩阵

`rand()`数字随机在 0 和 1 之间的矩阵

`diag()`对角阵

```matlab
% 矩阵 = diag(现有的矩阵，主对角线上方第k条斜线) 用行向量生成对角阵
matrix_1 = diag(matrix, 1)
matrix_1 = diag(matrix, 0)
matrix_1 = diag(matrix, -1)
```

函数 **tril** 生成下三角矩阵，或者使用 **triu** 函数生成上三角矩阵，具体使用代码的格式以下：

```matlab
% 矩阵 = tril(现有的矩阵，主对角线上第k条斜线) 让这条斜线上方的元素清零
% 矩阵 = triu(现有的矩阵，主对角线下第k条斜线) 让这条斜线下方的元素清零
matrix_1 = tril(matrix, 1)
matrix_1 = tril(matrix, 0)
matrix_1 = tril(matrix, -1)
matrix_1 = triu(matrix, 1)
matrix_1 = triu(matrix, 0)
matrix_1 = triu(matrix, -1)
```

`A+B %矩阵相加`
`C-B %矩阵相减`
`A*B %矩阵相乘`
`A.*B %矩阵对应元素相乘`

### 矩阵的函数运算

inv(B)=B<sup>-1</sup>
`A^n` VS `A.^n`
exp(A)=(exp(aij))
log(A)=(log(aij))
f(A)=(f(aij))
`A’=A/` 转置

### 矩阵的索引

- 位置标号引用

- 冒号运算符

## 矩阵的性能指标

| 指标   | 描述的矩阵性能                             |
| ------ | ------------------------------------------ |
| 二次型 | 正定性与负定性                             |
| 行列式 | 奇异性                                     |
| 特征值 | 奇异性、正定性，对角元素的结构             |
| 迹     | 对角元素之和，特征值之和                   |
| 秩     | 行(列)之间的线性无关性；线性方程组的适定性 |

## 特殊矩阵

每种特殊矩阵都与某类特殊问题相关

### 与单位矩阵密切相关的矩阵

置换矩阵、交换矩阵、互换矩阵、选择矩阵，这四种矩阵都只由0和1组成，每行每列都只有一个非零元素1，只是位置不同

#### 置换矩阵(permutation matrix)

- 每行每列恰好只有一个非零元素1的正方矩阵
- 左乘置换矩阵则重排行，右乘纵列（置换矩阵在右）经过置换后得到的矩阵
- 置换矩阵是正交矩阵

#### 互换矩阵(exchange matrix)

- 又称反射矩阵(reflection matrix)或后向单位矩阵(bachward identity matrix)
- 非零元素1全在反对角线上的特殊置换矩阵，常用符号J表示
- 左乘J则按行反转，右乘J则按列反转
- $J_{{n}}={\begin{pmatrix}0&0&\cdots &0&0&1\\0&0&\cdots &0&1&0\\0&0&\cdots &1&0&0\\\vdots &\vdots &&\vdots &\vdots &\vdots \\0&1&\cdots &0&0&0\\1&0&\cdots &0&0&0\end{pmatrix}}$

#### 移位矩阵(shift matrix)

#### 选择矩阵(selective matrix)

可以抽取(选择)给定向量(矩阵)的某些元素(行/列)的矩阵

### [正交矩阵](https://zh.wikipedia.org/wiki/正交矩阵)和[酉矩阵](https://zh.wikipedia.org/wiki/酉矩阵)

#### 正交矩阵(orthogonal matrix)

$Q^{T}=Q^{-1}\Leftrightarrow Q^{T}Q=QQ^{T}=I$

半正交矩阵(semi-orthogonal matrix)

Fourier、Hadamard matrix is orthogonal matrix

#### 酉矩阵(unitary matrix)

${\displaystyle U^{-1}=U^{*}\Leftrightarrow U^{*}U=UU^{*}=I_{n}}$

仿酉矩阵(para-unitary matrix)

#### 实矩阵 VS 复矩阵

| R                                                            | C                                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ${\displaystyle \|{\boldsymbol {x}}\|_{2}:={\sqrt {x_{1}^{2}+\cdots +x_{n}^{2}}}}$ | ${\|{\boldsymbol {z}}\|:={\sqrt {|z_{1}|^{2}+\cdots +|z_{n}|^{2}}}={\sqrt {z_{1}{\bar {z}}_{1}+\cdots +z_{n}{\bar {z}}_{n}}}}$ |
| $A^T=[a_{ji}]$     $(AB)^T=B^TA^T$                           | $A^H=[a_{ji}^*]$  $(AB)^H=B^HA^H$                            |
| $<x,y>=x^Ty$                                                 | $<x,y>=x^Hy$                                                 |
| $x^Ty$=0                                                     | $x^Hy=0$                                                     |
| $A^T=A$                                                      | $A^H=A$                                                      |
| $Q^T=Q^{-1}$                                                 | $U^H=U^{-1}$                                                 |
| $A=Q\Sigma Q^T=Q\Sigma Q^{-1}$                               | $A=U\Sigma U^T=U\Sigma U^{-1}$                               |
| $\|Qx\|=\|x\|$                                               | $\|Ux\|=\|x\|$                                               |
| $<Qx,Qy>=<x,y>$                                              | $<Ux,Uy>=<x,y>$                                              |

正交矩阵的逆矩阵即其转置；酉矩阵的逆矩阵即其共轭转置

正交矩阵是实数特殊化的酉矩阵；酉矩阵是实数上的正交矩阵在复数的推广

### 三角阵(upper/lower triangular matrix)

范德蒙矩阵(Vandermonde matrix)

${\displaystyle V={\begin{bmatrix}1&\alpha _{1}&\alpha _{1}^{2}&\dots &\alpha _{1}^{n-1}\\1&\alpha _{2}&\alpha _{2}^{2}&\dots &\alpha _{2}^{n-1}\\1&\alpha _{3}&\alpha _{3}^{2}&\dots &\alpha _{3}^{n-1}\\\vdots &\vdots &\vdots &\ddots &\vdots \\1&\alpha _{m}&\alpha _{m}^{2}&\dots &\alpha _{m}^{n-1}\\\end{bmatrix}}}$

傅立叶矩阵(Fourier matrix)

哈达玛矩阵(Hadamard matrix)

$HH^T=nI_n$

每个元素都是 +1 或 −1

每行都互相正交

${\displaystyle {\begin{aligned}H_{1}&={\begin{bmatrix}1\end{bmatrix}}\\H_{2}&={\begin{bmatrix}1&1\\1&-1\end{bmatrix}}\\H_{4}&={\begin{bmatrix}1&1&1&1\\1&-1&1&-1\\1&1&-1&-1\\1&-1&-1&1\end{bmatrix}}\end{aligned}}}$

托普利兹矩阵(Toeplitz matrix)，又称常对角矩阵
- 每条左上至右下的对角线均为常数的矩阵
- ${\displaystyle A={\begin{bmatrix}a_{0}&a_{-1}&a_{-2}&\ldots &\ldots &a_{-n+1}\\a_{1}&a_{0}&a_{-1}&\ddots &&\vdots \\a_{2}&a_{1}&\ddots &\ddots &\ddots &\vdots \\\vdots &\ddots &\ddots &\ddots &a_{-1}&a_{-2}\\\vdots &&\ddots &a_{1}&a_{0}&a_{-1}\\a_{n-1}&\ldots &\ldots &a_{2}&a_{1}&a_{0}\end{bmatrix}}}$

汉克尔矩阵(Hankel matrix)
- 每条右上至左下对角线均为常数的方阵
- 上下颠倒即得Toeplitz常对角矩阵
- ${\displaystyle H_{n}={\begin{pmatrix}a_{0}&a_{1}&a_{2}&\cdots &a_{n-1}\\a_{1}&a_{2}&a_{3}&\cdots &a_{n}\\\vdots &\vdots &\vdots &\ddots &\vdots \\a_{n-1}&a_{n}&a_{n+1}&\cdots &a_{2n-2}\\\end{pmatrix}}}$

### 特殊运算

#### 直和

$A\oplus B={\begin{bmatrix}A&0\\0&B\end{bmatrix}}$

#### Hadamard Product

也称为Schur积或对应元素乘积(elementwise product)

#### Kronecker Product

如果*A*是*m*×*n* 的矩阵，*B*是*p*×*q*的矩阵，**克罗内克积**则是一个*mp*×*nq*的[分块矩阵](https://zh.wikipedia.org/wiki/分塊矩陣)

$A\otimes B={\begin{bmatrix}a_{{11}}B&\cdots &a_{{1n}}B\\\vdots &\ddots &\vdots \\a_{{m1}}B&\cdots &a_{{mn}}B\end{bmatrix}}$

$A\otimes B={\begin{bmatrix}a_{{11}}b_{{11}}&a_{{11}}b_{{12}}&\cdots &a_{{11}}b_{{1q}}&\cdots &\cdots &a_{{1n}}b_{{11}}&a_{{1n}}b_{{12}}&\cdots &a_{{1n}}b_{{1q}}\\a_{{11}}b_{{21}}&a_{{11}}b_{{22}}&\cdots &a_{{11}}b_{{2q}}&\cdots &\cdots &a_{{1n}}b_{{21}}&a_{{1n}}b_{{22}}&\cdots &a_{{1n}}b_{{2q}}\\\vdots &\vdots &\ddots &\vdots &&&\vdots &\vdots &\ddots &\vdots \\a_{{11}}b_{{p1}}&a_{{11}}b_{{p2}}&\cdots &a_{{11}}b_{{pq}}&\cdots &\cdots &a_{{1n}}b_{{p1}}&a_{{1n}}b_{{p2}}&\cdots &a_{{1n}}b_{{pq}}\\\vdots &\vdots &&\vdots &\ddots &&\vdots &\vdots &&\vdots \\\vdots &\vdots &&\vdots &&\ddots &\vdots &\vdots &&\vdots \\a_{{m1}}b_{{11}}&a_{{m1}}b_{{12}}&\cdots &a_{{m1}}b_{{1q}}&\cdots &\cdots &a_{{mn}}b_{{11}}&a_{{mn}}b_{{12}}&\cdots &a_{{mn}}b_{{1q}}\\a_{{m1}}b_{{21}}&a_{{m1}}b_{{22}}&\cdots &a_{{m1}}b_{{2q}}&\cdots &\cdots &a_{{mn}}b_{{21}}&a_{{mn}}b_{{22}}&\cdots &a_{{mn}}b_{{2q}}\\\vdots &\vdots &\ddots &\vdots &&&\vdots &\vdots &\ddots &\vdots \\a_{{m1}}b_{{p1}}&a_{{m1}}b_{{p2}}&\cdots &a_{{m1}}b_{{pq}}&\cdots &\cdots &a_{{mn}}b_{{p1}}&a_{{mn}}b_{{p2}}&\cdots &a_{{mn}}b_{{pq}}\end{bmatrix}}$

考虑矩阵方程*AXB* = *C*，其中*A*、*B*和*C*给定，*X*未知

由${\displaystyle (B^{T}\otimes A)\,\operatorname {vec} (X)=\operatorname {vec} (AXB)=\operatorname {vec} (C)}$，可以推出：方程*AXB* = *C*具有唯一的解，当且仅当*A*和*B*是非奇异矩阵

#### Khatri-Rao Product

${\displaystyle \mathbf {A} \ast \mathbf {B} =\left(\mathbf {A} _{ij}\otimes \mathbf {B} _{ij}\right)_{ij}}$

### Matlab函数

- dot(X, Y, [DIM])
  - 

- diag()
  - diag(V, k=0) return a diagonal matrix with vector V on the K-th diagonal
  - diag(V, M, N) return a diagonal matrix of size MxN with vector V on the main diagonal
  - diag(A, k=0) extract K-th diagonal of the matrix A
- triu()
  
  - triu(X, k=0, [pack]) 
- vec()
- 
- hadamard(N)
  - return a Hn of size N-by-N
  - N must be 2^k*p, in which p is 1, 12, 20 or 28
- hankel()
  - hankel(C, [R]) return the Hankel matrix constructed from the first column C, and
         (optionally) the last row R 
  - ```H(i,j) = c(i+j-1),  i+j-1 <= m;H(i,j) = r(i+j-m),  otherwise```
- blkdiag(A, B, C, ...) 直和
- circshift() 循环平移数组
  - cirshift(X, N, dim=1)
    - cirshift(X, [0,1]) equals to cirshift(X, 1, 2)
- flipud() fliplr() 上下左右翻转