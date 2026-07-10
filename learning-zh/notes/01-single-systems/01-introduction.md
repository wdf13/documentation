# 1.1 Single systems — Introduction

> 课程：Basics of Quantum Information  
> 单元：Single systems  
> 原始内容：`learning/courses/basics-of-quantum-information/single-systems/introduction.ipynb`

## 1. 本节要解决的问题

本节建立量子信息课程最基础的分析框架：

```math
\text{状态}
\longrightarrow
\text{操作}
\longrightarrow
\text{测量}
```

需要回答三个问题：

1. 如何描述系统当前的状态？
2. 如何描述系统状态的变化？
3. 如何从系统中读取信息？

## 2. 本节在课程中的位置

当前只研究一个孤立系统，不讨论多个系统之间的相关性与纠缠。

课程整体顺序为：

```math
\text{单系统}
\longrightarrow
\text{复合系统}
\longrightarrow
\text{量子电路}
\longrightarrow
\text{纠缠协议}
```

## 3. 原文核心内容

本节介绍：

- 使用复数向量描述量子态；
- 使用酉矩阵描述理想量子操作；
- 通过测量从量子态中提取经典信息；
- 当前只讨论单个系统；
- 下一单元再推广到多个相互作用或相关的系统。

## 4. 中文语义解释

### 4.1 系统

这里的系统是抽象的信息载体，例如经典比特、电子自旋、光子偏振或超导量子比特。

课程暂时忽略具体物理实现，只保留与信息处理有关的数学结构。

### 4.2 单系统

单系统表示当前只研究一个独立的信息系统。例如一个量子比特：

```math
|\psi\rangle
=
\alpha|0\rangle+\beta|1\rangle
```

暂时不讨论它是否与其他量子比特纠缠。

## 5. 状态

经典概率状态可以写为：

```math
p=
\begin{pmatrix}
p_0\\
p_1
\end{pmatrix}
```

并满足：

```math
p_0\geq0,\qquad
p_1\geq0,\qquad
p_0+p_1=1
```

量子比特状态写为：

```math
|\psi\rangle
=
\alpha|0\rangle+\beta|1\rangle
```

其中：

```math
\alpha,\beta\in\mathbb{C}
```

并满足：

```math
|\alpha|^2+|\beta|^2=1
```

量子态系数是概率振幅，不是概率。真正的测量概率为：

```math
P(0)=|\alpha|^2,\qquad
P(1)=|\beta|^2
```

## 6. 操作

理想封闭量子系统的演化由酉矩阵表示：

```math
|\psi'\rangle=U|\psi\rangle
```

酉矩阵满足：

```math
U^\dagger U=I
```

因此：

```math
\langle\psi'|\psi'\rangle
=
\langle\psi|U^\dagger U|\psi\rangle
=
\langle\psi|\psi\rangle
```

所以酉演化保持归一化。

酉演化还具有：

- 保持内积；
- 保持正交性；
- 可逆，且 `U^{-1}=U^\dagger`。

## 7. 测量

对于量子态：

```math
|\psi\rangle
=
\alpha|0\rangle+\beta|1\rangle
```

在计算基中测量时：

```math
P(0)=|\alpha|^2
```

```math
P(1)=|\beta|^2
```

单次测量只会得到经典结果 `0` 或 `1`。

因此测量实现：

```math
\text{量子信息}
\longrightarrow
\text{经典信息}
```

在只观察被测系统的有效描述中，测量通常是非酉且不可逆的。把系统、测量仪器和环境一起考虑时，它们在更大空间中的相互作用仍可由酉演化描述。

## 8. 归一化推导

设：

```math
|\psi\rangle
=
\alpha|0\rangle+\beta|1\rangle
```

则：

```math
\langle\psi|
=
\alpha^*\langle0|+\beta^*\langle1|
```

利用：

```math
\langle0|0\rangle=1,\qquad
\langle1|1\rangle=1
```

以及：

```math
\langle0|1\rangle=0,\qquad
\langle1|0\rangle=0
```

得到：

```math
\langle\psi|\psi\rangle
=
|\alpha|^2+|\beta|^2
```

合法量子态要求：

```math
\langle\psi|\psi\rangle=1
```

其含义是所有可能测量结果的总概率等于 `1`。

## 9. 相对相位例子

考虑：

```math
|\psi_+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt{2}}
```

和：

```math
|\psi_-\rangle
=
\frac{|0\rangle-|1\rangle}{\sqrt{2}}
```

它们在计算基中的测量概率都为：

```math
P(0)=P(1)=\frac12
```

但它们不是同一个量子态。经过 Hadamard 门后：

```math
H|\psi_+\rangle=|0\rangle
```

```math
H|\psi_-\rangle=|1\rangle
```

这说明概率振幅的符号和相位会影响干涉结果。

## 10. Qiskit 最小示例

```python
from qiskit import QuantumCircuit
from qiskit.quantum_info import Statevector

plus = QuantumCircuit(1)
plus.h(0)

minus = QuantumCircuit(1)
minus.x(0)
minus.h(0)

plus_state = Statevector.from_instruction(plus)
minus_state = Statevector.from_instruction(minus)

print("plus state:", plus_state)
print("minus state:", minus_state)
print("plus probabilities:", plus_state.probabilities_dict())
print("minus probabilities:", minus_state.probabilities_dict())
```

## 11. 易错点

1. 概率振幅不是概率，概率由振幅模平方得到。
2. 测量不会直接输出完整态向量。
3. 两个状态在某一组基中的测量概率相同，不代表它们是同一个状态。
4. 酉矩阵不仅保持范数，还保持内积并保证演化可逆。
5. 被测系统的有效测量过程通常不是酉演化。

## 12. 自测题

### 概念题

为什么量子态中的系数不能直接称为概率？

### 计算题

判断下面的状态是否归一化：

```math
|\psi\rangle
=
\frac12|0\rangle
+
\frac{\sqrt3}{2}|1\rangle
```

### 推导题

证明酉演化保持两个量子态之间的内积。

### 判断题

判断并说明理由：

1. 两个量子态在计算基中的测量概率相同，因此它们一定相同。
2. 量子测量在被测系统的有效描述中通常不可逆。
3. 任意普通矩阵都可以描述封闭量子系统的演化。
4. 酉演化保持量子态归一化。

### Qiskit 编程题

分别构造：

```math
|\psi_+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2}
```

和：

```math
|\psi_-\rangle
=
\frac{|0\rangle-|1\rangle}{\sqrt2}
```

输出两个态向量及其计算基测量概率，再分别施加 Hadamard 门，验证最终状态。

## 13. 本节总结

```math
\boxed{
\text{量子信息系统}
=
\text{状态}
+
\text{操作}
+
\text{测量}
}
```

其中：

```math
\text{状态}\leftrightarrow\text{单位复向量}
```

```math
\text{操作}\leftrightarrow\text{酉矩阵}
```

```math
\text{测量}\leftrightarrow\text{从量子态产生经典结果}
```

## 14. 本节上下文摘要

本节建立单量子系统的状态—操作—测量框架。量子态由单位复向量表示，封闭系统的理想演化由酉矩阵描述，测量把量子信息转换为经典结果。概率振幅的模平方才是测量概率。

## 15. 来源说明

本笔记基于 IBM Quantum / Qiskit Documentation 的 `Basics of Quantum Information` 课程整理，仅用于个人学习，不是官方中文译本。
