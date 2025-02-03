# Groups

## 群的定义
群是一个集合$G$，配备一个二元运算$\cdot$，满足下面几个性质：
- （G0）封闭性：对于所有 $a, b \in G$，有 $a \cdot b \in G$。
- （G1）结合律：对于所有 $a, b, c \in G$，有 $(a \cdot b) \cdot c = a \cdot (b \cdot c)$。
- （G2）单位元：存在 $e \in G$，使得对于所有 $a \in G$，有 $e \cdot a = a \cdot e = a$。
- （G3）逆元：对于每个 $a \in G$，存在 $b \in G$，使得 $a \cdot b = b \cdot a = e$，其中$b$记为$a^{-1}$。
## 阿贝尔群定义
如果群的二元运算还满足交换律，即 $a \cdot b = b \cdot a$，则 $G$ 是阿贝尔群。

$$
\boxed{\text{实数集 } \mathbb{R} \text{ 在加法下是阿贝尔群，且 } \mathbb{R}^* = \mathbb{R} - {0} \text{ 在乘法下也是阿贝尔群。}}
$$
```{note}
0在乘法下不存在逆元，不满足群的定义。
```
````{margin}
```{note}
当集合仅满足G0,G1和G2时，被称为半群（monoid），例如自然数集合在加法运算下，难以找到逆元，因此不属于群，但属于半群。
```
````
