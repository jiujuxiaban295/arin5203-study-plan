# ARIN5203 Cheatsheet 索引

> 渐进式披露：**这一页只放"题目长什么样 → 一行答案 → 去哪张卡"**。卡片放步骤、公式、陷阱；卡片末尾的"讲义出处"直接链到讲义 PDF 的那一页。考场上先看这页，不够再点卡，再不够再点讲义。  
> 讲义链接指向[课程网站](https://cqf.io/ARIN5203/lectures/index.html)（去年规则允许浏览课程网站及其外链，禁止其他外部网站；GitHub 不算课程网站）。`#page=N` 是 PDF 阅读器页码，和本仓库所有页码一致；若考场断网，提前下载同名 PDF，按同样页码翻。今年规则以教师通知为准。  
> 哪些内容必须练到不查也会、哪些查卡即可，见[Cheatsheet 规划与必练清单](../cheatsheet规划与必练清单.md)。

## 一、计算卡（先独立算，卡只用来核对）

| 题目长什么样 | 一行答案 | 卡 |
|---|---|---|
| 给 N、F、S、P，问输出尺寸／哪些尺寸可能 | (N + 2P − F)/S + 1，除不尽向下取整 | [CNN](计算/CNN.md) |
| 给核大小、通道、核数，问参数量 | (F·F·C + 1)·K，与图片大小无关 | [CNN](计算/CNN.md) |
| L 层 F×F、步长 1，问感受野 | 1 + L(F − 1)；含步长用递推 r ← r + (F−1)·j，j ← j·S | [CNN](计算/CNN.md) |
| 多头自注意力，n、d、h，问时间复杂度 | O(n²d + nd²)，h 约掉；只给 Q/K/V 或 n ≫ d 答 O(n²d) | [Attention](计算/Attention.md) |
| 问注意力参数量 | Q、K、V 共 3d²（加输出投影 4d²），与 n 无关；含 bias 再加 4d | [Attention](计算/Attention.md) |
| 给 q(x_t\|x_{t−1}) = N(√(1−β)x_{t−1}, βI)，问方差 | (1−β)·Var(x_{t−1}) + β·I；旧方差 I → I | [Diffusion 方差](计算/Diffusion方差.md) |
| f(x) = W₂ReLU(W₁x)，L = ‖f − y‖²，求 ∂L/∂x | 2(f − y)ᵀ·W₂·diag(z > 0)·W₁，按形状链核对 | [矩阵求导](计算/矩阵求导.md) |
| 线性隐藏层网络，问能否化简、写 A、B、C | 代入 → 拆括号 → 合并同类项；线性能化简，分段线性不能 | [网络化简与梯度比例](计算/网络化简与梯度比例.md) |
| 问 ∂L/∂w₁ : ∂L/∂w₃ : ∂L/∂w₅ | 同一神经元的权重梯度 ∝ 各自输入：1 : x₁ : x₂ | [网络化简与梯度比例](计算/网络化简与梯度比例.md) |

## 二、概念表卡（查了就能答）

| 题目长什么样 | 一行答案 | 卡 |
|---|---|---|
| 哪两类生成模型能算精确密度 | 自回归（链式法则连乘）、normalizing flow（变量替换） | [生成模型五类](概念/生成模型五类.md) |
| VAE／GAN 的特点、怎么训练 | VAE：encoder 出 μ、Σ，重建 − KL，无标签；GAN：两网络对抗 | [生成模型五类](概念/生成模型五类.md) |
| diffusion 流程、训练预测什么、采样几步 | 加噪固定，去噪可学，预测噪声，采样 T 步 | [Diffusion／Flow matching／CFG／LDM](概念/Diffusion-FlowMatching-CFG-LDM.md) |
| flow matching／rectified flow 是什么 | 噪声到数据走直线 x_t = (1−t)x + tz，网络预测速度 z − x | 同上 |
| CFG 是什么、哪些模型能用 | v_cfg = (1+w)v_y − w·v_∅；diffusion、rectified flow 能，GAN、VAE 不能 | 同上 |
| latent diffusion 是什么 | VAE 压成 latent → 在 latent 上扩散 → decoder 还原；encoder 冻结 | 同上 |
| BERT／GPT／T5 怎么预训练、各擅长什么 | 填空／预测下一词／挖段还原；理解／生成／输入一段出一段 | [预训练与三种架构](概念/预训练与三种架构.md) |
| transfer learning、ICL、scaling law | 预训练＋微调；例子进 prompt 不改参数；成本 ∝ 参数×token，配平 | [预训练与三种架构](概念/预训练与三种架构.md) · [微调／ICL／RAG／Scaling](概念/微调-ICL-RAG-Scaling.md) |
| reward model 是什么、DPO 的好处、DPO 用什么反馈 | 学出来的偏好预测器；去掉 reward model；二元偏好 | [对齐 SFT／RLHF／DPO](概念/对齐-SFT-RLHF-DPO.md) |
| instruction tuning 的目的 | 适应特定数据，同时保留通用能力 | 同上 |
| RAG 是什么、和微调怎么选 | 检索段落进 prompt，不改参数，知识可更新；会变的知识用 RAG | [微调／ICL／RAG／Scaling](概念/微调-ICL-RAG-Scaling.md) |
| RNN／LSTM／self-attention／transformer 谁置换不变、省内存、可并行 | 置换不变：attention、transformer；省内存：RNN、LSTM；并行：attention、transformer；attention 可进 CNN | [序列模型比较](概念/序列模型比较.md) |
| 位置编码是什么、固定随机能不能用 | 注入顺序，因 self-attention 无序；固定随机可以，每步重抽不行 | [序列模型比较](概念/序列模型比较.md) |
| 多模态 LLM 特点、CLIP、LLaVA、ViT | 三件套；对比学习；视觉编码器冻结；patch 当 token、更吃数据 | [多模态与 VLA](概念/多模态与VLA.md) |
| 哪些函数不能当激活函数、过拟合怎么办 | 线性的、定义域不全的不行；数据增强、早停、dropout、减小模型 | [激活函数／损失／过拟合](概念/激活函数-损失-过拟合.md) |
| NeRF／Gaussian Splatting 特点 | MLP 表示体积场景、坐标先位置编码；高斯带颜色与不透明度 | [NeRF／GS](概念/NeRF-GS.md) |

## 图解

[Diffusion 与多模态图解](图解/diffusion与多模态.html)：加雾／擦雾时间线、训练与采样循环、方差保持、多模态三件套、CLIP 配对矩阵、LLaVA 冻结图。在线版 https://claude.ai/artifact/QCcaEWea7k6izudjB3yrpa（考场若禁外站，提前把 HTML 存到本地用浏览器打开）。

[Flow Matching、CFG 与 LDM 图解](图解/流匹配CFG与LDM.html)：直线路径 vs 弯路、CFG 放大差值的向量图、latent diffusion 三步、RNN 顺序读 vs attention 摊开看、VLA 把动作当文字。在线版 https://claude.ai/artifact/HznhhD5AMX36Qsguarpu5G。

## 三、多选陷阱词

见 [陷阱词](陷阱词.md)：限制词排除、能力陈述偏宽通常对、生成模型"需要标签"永远错，等等。

## 使用顺序（考场）

1. 读题，找上表最像的一行，看一行答案够不够。
2. 不够：点卡，按"触发 → 步骤 → 公式 → 陷阱"走。
3. 再不够：点卡末尾的讲义页。
4. 计算题先自己算，卡只核对；单题卡住超过 4 分钟先跳过。
