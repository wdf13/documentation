# 1.2 Single systems — Classical information

> 课程：Basics of Quantum Information  
> 单元：Single systems  
> 原始内容：`learning/courses/basics-of-quantum-information/single-systems/classical-information.ipynb`

## 1. 本节目标

本节通过经典信息建立量子信息的参照框架：

```math
\text{经典状态}
\longrightarrow
\text{概率向量}
\longrightarrow
\text{经典测量}
\longrightarrow
\text{确定性操作}
\longrightarrow
\text{随机矩阵}
```

## 2. 经典状态集合

记系统为 `X`，其经典状态集合为：

```math
\Sigma
```

本课程要求 `Σ` 是有限且非空的。

例如，比特满足：

```math
\Sigma=\{0,1\}
```

六面骰子满足：

```math
\Sigma=\{1,2,3,4,5,6\}
```

经典状态是能够被无歧义识别的系统配置。

## 3. 确定性状态

若系统确定处于状态 `a`，用标准基向量表示：

```math
|a\rangle
```

对于比特：

```math
|0\rangle=
\begin{pmatrix}
1\\
0
\end{pmatrix},
\qquad
|1\rangle=
\begin{pmatrix}
0\\
1
\end{pmatrix}
```

## 4. 概率状态

若我们不能确定系统处于哪个经典状态，可使用概率向量：

```math
p=
\begin{pmatrix}
p_0\\
p_1\\
\vdots\\
p_{n-1}
\end{pmatrix}
```

合法概率向量满足：

```math
p_i\geq0
```

以及：

```math
\sum_i p_i=1
```

例如：

```math
p=
\begin{pmatrix}
\frac34\\
\frac14
\end{pmatrix}
=
\frac34|0\rangle+\frac14|1\rangle
```

概率向量中的位置必须和状态集合的排列顺序一致。

## 5. 经典测量

测量概率状态时，我们不会直接观察到整个概率向量，而只会得到一个确定的经典结果。

若：

```math
p=
\begin{pmatrix}
\frac34\\
\frac14
\end{pmatrix}
```

则得到 `0` 和 `1` 的概率分别为 `3/4` 和 `1/4`。

若测量得到 `1`，我们将知识更新为：

```math
|1\rangle=
\begin{pmatrix}
0\\
1
\end{pmatrix}
```

经典概率状态通常描述观察者的知识或信念：

```math
\text{经典不确定性}\neq\text{量子叠加}
```

## 6. Dirac notation

### 6.1 Ket

```math
|a\rangle
```

表示列向量。

### 6.2 Bra

```math
\langle a|
```

表示行向量。对于复向量：

```math
\langle\psi|
=
\left(|\psi\rangle\right)^\dagger
```

### 6.3 内积

```math
\langle a|b\rangle
```

是标量。标准基满足：

```math
\langle a|b\rangle
=
\begin{cases}
1,&a=b\\
0,&a\neq b
\end{cases}
```

### 6.4 外积

```math
|b\rangle\langle a|
```

是矩阵。例如：

```math
|0\rangle\langle1|
=
\begin{pmatrix}
0&1\\
0&0
\end{pmatrix}
```

它将 `|1>` 映射到 `|0>`，将 `|0>` 映射到零向量。

## 7. 确定性操作

确定性操作由函数表示：

```math
f:\Sigma\rightarrow\Sigma
```

对应矩阵满足：

```math
M|a\rangle=|f(a)\rangle
```

并可写为：

```math
M=
\sum_{a\in\Sigma}|f(a)\rangle\langle a|
```

因为：

```math
M|b\rangle
=
\sum_{a\in\Sigma}|f(a)\rangle\langle a|b\rangle
=
|f(b)\rangle
```

对于比特，四种确定性操作分别为：

### 恒为 0

```math
M=
\begin{pmatrix}
1&1\\
0&0
\end{pmatrix}
```

### 恒等操作

```math
M=
\begin{pmatrix}
1&0\\
0&1
\end{pmatrix}
```

### NOT 操作

```math
M=
|1\rangle\langle0|
+
|0\rangle\langle1|
=
\begin{pmatrix}
0&1\\
1&0
\end{pmatrix}
```

### 恒为 1

```math
M=
\begin{pmatrix}
0&0\\
1&1
\end{pmatrix}
```

确定性操作矩阵每一列恰好有一个 `1`，其余元素为 `0`。

## 8. 概率操作与随机矩阵

概率操作允许同一输入产生多个可能输出。

例如：

```math
M=
\begin{pmatrix}
1&\frac12\\
0&\frac12
\end{pmatrix}
```

表示：

- 输入 `0` 时一定输出 `0`；
- 输入 `1` 时，以 `1/2` 概率输出 `0`，以 `1/2` 概率输出 `1`。

本课程采用列概率向量：

```math
p'=Mp
```

因此列随机矩阵必须满足：

```math
M_{ij}\geq0
```

以及：

```math
\sum_iM_{ij}=1
\qquad
\text{对每一列 }j
```

## 9. 为什么随机矩阵保持概率向量

输出分量为：

```math
p'_i=\sum_jM_{ij}p_j
```

因为所有元素非负，所以：

```math
p'_i\geq0
```

总概率为：

```math
\sum_i p'_i
=
\sum_j
\left(\sum_iM_{ij}\right)p_j
=
\sum_jp_j
=
1
```

因此：

```math
p\text{ 是概率向量}
\Longrightarrow
Mp\text{ 仍是概率向量}
```

## 10. 确定性操作与概率操作的关系

每个确定性操作矩阵都是随机矩阵，所以：

```math
\text{确定性操作}\subset\text{概率操作}
```

但一般随机矩阵的每列可以包含多个非零概率。

## 11. 概率操作的组合

若先执行 `M`，再执行 `N`：

```math
p'=Mp
```

```math
p''=Np'=N(Mp)=(NM)p
```

两个随机矩阵的乘积仍是随机矩阵。

## 12. 不变分布

考虑：

```math
M=
\begin{pmatrix}
0.8&0.3\\
0.2&0.7
\end{pmatrix}
```

以及：

```math
p=
\begin{pmatrix}
0.6\\
0.4
\end{pmatrix}
```

有：

```math
Mp=
\begin{pmatrix}
0.6\\
0.4
\end{pmatrix}
=p
```

所以 `p` 是 `M` 的不变分布或平稳分布。

从线性代数角度看：

```math
Mp=1\cdot p
```

因此 `p` 是对应特征值 `1` 的特征向量，并且已经概率归一化。

## 13. Python 实现

```python
import numpy as np

M = np.array([
    [0.8, 0.3],
    [0.2, 0.7],
], dtype=float)

p = np.array([0.6, 0.4], dtype=float)
p_next = M @ p

assert np.all(M >= 0)
assert np.allclose(M.sum(axis=0), 1.0)
assert np.all(p >= 0)
assert np.isclose(p.sum(), 1.0)
assert np.allclose(p_next, p)

print(p_next)
```

注意：经典概率向量不能直接当作 Qiskit `Statevector`，因为量子态分量是概率振幅，测量概率由振幅模平方给出。

## 14. 易错点

1. 随机矩阵不仅要求每列和为 `1`，还要求所有元素非负。
2. 本课程采用列向量，所以要求每列和为 `1`。
3. 经典概率状态不等于量子叠加。
4. `bra × ket` 得到标量，`ket × bra` 得到矩阵。
5. 确定性操作不一定可逆。
6. 状态排列顺序决定向量各分量的位置。
7. `Mp=p` 不代表 `M` 是恒等矩阵，而是说明 `p` 是不变分布。

## 15. 自测题

1. 判断下面向量是否为合法概率向量：

```math
\begin{pmatrix}
0.5\\
-0.2\\
0.7
\end{pmatrix}
```

2. 计算：

```math
\langle0|1\rangle
```

以及：

```math
|1\rangle\langle0|
```

3. 给定：

```math
f(0)=1,\qquad f(1)=1
```

构造对应确定性操作矩阵。

4. 判断：

```math
M=
\begin{pmatrix}
0.6&0.2\\
0.4&0.8
\end{pmatrix}
```

是否为合法列随机矩阵。

5. 求满足下式的概率向量：

```math
Mp=p
```

其中：

```math
M=
\begin{pmatrix}
0.9&0.2\\
0.1&0.8
\end{pmatrix}
```

## 16. 本节总结

```math
\boxed{
\text{经典信息}
=
\text{概率向量}
+
\text{随机矩阵}
+
\text{经典测量}
}
```

其中：

```math
\text{确定性状态}\leftrightarrow\text{标准基向量}
```

```math
\text{确定性操作}\leftrightarrow\text{每列恰有一个 }1\text{ 的矩阵}
```

```math
\text{概率操作}\leftrightarrow\text{列随机矩阵}
```

## 17. 本节上下文摘要

本节学习了经典状态集、概率向量、经典测量、Dirac notation、确定性操作和随机矩阵。概率向量分量非负且总和为一；随机矩阵元素非负且每列和为一，因此能将合法概率状态映射为合法概率状态。

## 18. 来源说明

本笔记基于 IBM Quantum / Qiskit Documentation 的 `Basics of Quantum Information` 课程整理，仅用于个人学习，不是官方中文译本。
