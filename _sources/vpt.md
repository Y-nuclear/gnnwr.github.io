# Visual Prompt Tuning

- 文章链接：[Visual Prompt Tuning](https://arxiv.org/abs/2203.12119)
- Github：[kmnp/vpt](https://github.com/kmnp/vpt)
- 时间：2022

## 摘要

当前采用预训练模型的做法涉及更新所有骨干参数，即完全微调（Full）。本文引入视觉提示调谐( Visual Prompt Tuning，VPT )作为视觉上大规模Transformer模型全微调的一种高效有效的替代方案。**受启发于最近在高效调优大型语言模型方面的进展**，VPT在保持模型主干冻结的同时，仅在输入空间中引入少量可训练参数(小于模型参数的1\%)。通过在各种下游识别任务上的大量实验，我们表明，与其他参数有效的调优协议相比，VPT取得了显著的性能增益。最重要的是，在许多情况下，VPT甚至优于完全微调。

![VPT summary](./VPT/image.png)

## 模型/方法

### VIT

对于具有N层的ViT，将输入图像划分为m个固定大小的Patch $\{ I_j∈R^{3 × h × w} | j∈N，1≤j≤m \}$，h，w为图像块的高度和宽度。然后，每个Patch首先通过Embed和位置编码嵌入到D维隐空间中：

$$
\begin{align}
e_{0}^j = Embed(I_j)
\end{align}
$$

将Embed的集合记为$E_i$,并引入分类标记头[CLS]记为$x_i$,则可以将ViT视为如下表达式：

$$
[x_i,E_i] = L_i([x_{i-1},E_{i-1}])\\
y = Head(x_N)
$$

### VPT

对于一个已经完成预训练的Transformer模型，VPT在Embed层后引入一组p个D维连续embedding，即提示。在微调期间仅更新任务特定的提示，而保持Transformer的主干冻结。

#### VPT-Shallow

VPT-Shallow仅在第一个Transformer前加入提示，记第一个提示为$P$，则shallow-prompt ViT可以记为:

$$
[x_1,Z_1,E_1] = L_1([x_0,P,E_0])\\
[x_i,Z_i,E_i] = L_i([x_{i-1},Z_{i-1},E_{i-1}])\\
y=Head(x_N)
$$

其中仅有P和Head为可学习参数。

#### VPT-Deep

VPT-Deep在每层Transformer输入空间中引入Prompt，将每层输入的可学习提示记为$P_i$，则Deep-prompt ViT可以记为:

$$
[x_i,Z_i,E_i] = L_i([x_{i-1},P_{i-1},E_{i-1}])\\
y=Head(x_N)
$$

其中每层的$P_i$直接引入，不受transformer输出的影响，同时其与Head为可学习参数。

#### VPT-swin

在Swin中，VPT提示仅在窗口中被关注，在Patch Merging阶段被忽略。

## 实验结果

![对比实验结果1](./VPT/result_1.png)
![对比实验结果2](./VPT/result_2.png)

VPT-Deep在多个任务里要好于完全微调，在适应较大的Transformer中是一个有较大潜力的方法。VPT-Shallow要次于Deep，但在存储受限的条件下仍然有较大的潜力。
