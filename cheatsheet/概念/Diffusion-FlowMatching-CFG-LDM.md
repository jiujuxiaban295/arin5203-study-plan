# 概念卡 · Diffusion、Flow matching、CFG、Latent diffusion

**触发：** 题干出现 forward／reverse process、noise schedule、denoising、U-Net、rectified flow、velocity、classifier-free guidance、guidance scale、latent、Stable Diffusion、DiT、text-to-image／video。方差计算见[计算卡](../计算/Diffusion方差.md)。

## Diffusion（DDPM）流程卡

```
正向（固定，无参数）  x₀ 真图 → 每步 x_t = √(1−β_t)·x_{t−1} + √β_t·ε → x_T ≈ N(0, I)；β_t 预先定好（线性表）
反向（可学）          网络 ε_θ(x_t, t) 猜"这一步加进去的噪声"；U-Net，t 用正弦位置编码送入
训练                  抽 x₀、抽 t、一步跳到 x_t（闭式 ᾱ_t）、损失 ‖ε − ε_θ(x_t, t)‖²；无标签
采样                  x_T ~ N(0, I) → 每步减掉猜的噪声（再撒一点新噪声）→ T 步到 x₀；慢
```

## Flow matching／Rectified flow

```
路径随便选，只要起点噪声、终点数据；最简单是直线：x_t = (1−t)·x + t·z   （Lecture 12 约定：t=0 数据，t=1 噪声）
训练   抽 x、z、t；网络预测速度 v = z − x；损失 ‖f_θ(x_t, t) − v‖²
采样   从 z 出发，T 步 Euler：x ← x − f_θ(x_t, t)/T（T 常 50）
关系   DDPM = 方差保持路径、预测噪声；flow matching = 直线路径、预测速度；预测噪声／速度／干净图可互换
注意   Lecture 9 约定相反（x₀ 噪声、x₁ 数据，速度 x₁ − x₀，x += dt·v）；看题目定义
```

## Classifier guidance vs Classifier-free guidance

| | Classifier guidance | **CFG** |
|---|---|---|
| 额外模型 | 要训一个在噪声图上的分类器 p(y\|x_t) | 不要；训练时随机把条件 y 丢成 ∅（约 10–30%），同一模型既会条件也会无条件 |
| 采样 | 用分类器梯度推方向 | v_cfg = (1+w)·v_y − w·v_∅（等价 ε_cfg = s·(ε_c − ε_∅) + ε_∅，s = 1+w） |
| 缺点 | 分类器对噪声图分布外 | 每步算两次，采样成本翻倍 |

- w = 0 普通条件生成；w 越大越贴文字，保真与多样性下降。
- **适用**：逐步预测噪声／速度的模型，即 diffusion、rectified flow／flow matching。**不适用**：GAN、VAE（一步出图，没有可叠加的逐步预测）。

## Latent diffusion（LDM）

```
① 训 VAE encoder/decoder：图 H×W×3 → latent (H/D)×(W/D)×C，常 D=8、C=16（256×256×3 → 32×32×16）
   decoder 模糊 → 加 GAN 判别器一起训；KL 权重很小 → "VAE + GAN + diffusion"
② 冻结 encoder，在 latent 上训扩散（预测噪声或速度）
③ 生成：抽随机 latent → 迭代去噪 → decoder 还原成图
文生图：文本编码器（T5／CLIP）→ 去噪网络用 Transformer（DiT）；t 用 scale/shift 注入，文本用 cross-attention
视频：latent 多一维时间 t×h×w×c，加时间方向注意力／卷积
```

## 陷阱

- "正向过程有参数""训练预测干净图""采样一步出图""β_t 学出来的"都错（默认口径）。
- CFG 不需要分类器；"CFG 可用于 GAN"错。
- LDM 训扩散时 encoder 冻结；decoder 只在最后用。
- Q2.8 精确密度不写 diffusion 也不写 flow matching。

## 讲义出处

- 图解（六张示意图）：[cheatsheet/图解/diffusion与多模态.html](../图解/diffusion与多模态.html)，在线版 https://claude.ai/artifact/QCcaEWea7k6izudjB3yrpa
- DDPM 两过程、训练、采样：[Lecture 8 第 51–60 页](https://cqf.io/ARIN5203/lectures/Lecture8.pdf#page=51)；网络与 t 嵌入：[第 61 页](https://cqf.io/ARIN5203/lectures/Lecture8.pdf#page=61)；噪声表：[第 62 页](https://cqf.io/ARIN5203/lectures/Lecture8.pdf#page=62)
- 直觉版：[Lecture 12 第 4–7 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=4)
- Rectified flow 训练与采样：[Lecture 12 第 8–23 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=8)；flow matching 路径自由：[Lecture 9 第 42–50 页](https://cqf.io/ARIN5203/lectures/Lecture9.pdf#page=42)
- Classifier guidance／CFG：[Lecture 8 第 72–74 页](https://cqf.io/ARIN5203/lectures/Lecture8.pdf#page=72)、[Lecture 12 第 28–38 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=28)、[Lecture 9 第 93–97 页](https://cqf.io/ARIN5203/lectures/Lecture9.pdf#page=93)
- LDM：[Lecture 12 第 51–63 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=51)；DiT 与文生图：[第 64–68 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=64)；视频：[第 69–71 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=69)、[Lecture 8 第 76–78 页](https://cqf.io/ARIN5203/lectures/Lecture8.pdf#page=76)
