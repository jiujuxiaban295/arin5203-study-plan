# 概念卡 · ViT、多模态 LLM、CLIP／Flamingo／LLaVA、VLA、图像／视频生成

**触发：** 题干出现 Vision Transformer、patch、multimodal LLM、CLIP、contrastive、zero-shot、LLaVA、Flamingo、VLA、robot action、RT-2、text-to-image／video。

## ViT

- 图切成 p×p patch → 拉直（3·p·p 个数）→ 线性投影到 D 维 → 加可学习位置向量 → 加 class token → 标准 Transformer encoder。224/16 = 14，196 个 token（加 class token 197）。
- **比 CNN 更吃数据**：只在 ImageNet 从头训不如 ResNet，JFT-300M 预训练后反超。不只做分类，也做检测、分割。

## 多模态 LLM 三件套

| 部件 | 输入 → 输出 | 备注 |
|---|---|---|
| 图像编码器（ViT） | 图 → 一串图像向量（每 patch 一个） | 常用 CLIP 预训练过的 |
| Projector／connector | 图像向量 → LLM 词向量空间 | 一两层线性 |
| LLM（decoder） | 图像 token + 文字 token → 文字 | LLM 不知道自己在看图 |

训练目标：**以图像和文本 token 为条件的语言建模**。数据：图文对、视觉指令数据、图文交错文档。

- **CLIP**：图像编码器 + 文本编码器，**对比损失**学正确配对；测试时可**丢掉文本编码器**，图像编码器做 zero-shot 分类与图文检索。不是分类交叉熵，不是 RLHF。
- **Flamingo**：预训练视觉编码器 + 语言模型，吃任意交错图文，多模态 in-context learning。
- **LLaVA**：两阶段（对齐预训练 → 有监督微调），**视觉编码器冻结**，只更新 projector 和 LLM。
- 特点：能处理多种模态、提升多数据类型任务；本课口径下"能处理和生成文本、图像、动作"判对。挑战：语言偏差，不看图也能答。

## VLA

- 定义：从语言指令 + 视觉信号**直接生成机器人可执行动作**。
- 分层（工业：感知与决策分开训，动作限于技能库）vs 端到端（学术：一步出动作）。
- RT-2：动作写成数字文本串，当翻译任务；55B，ViT + PaLM，强语义推理。OpenVLA：7B，DINOv2 + SigLIP + Llama-7B，快速微调。动作头也可用 diffusion policy／ACT。LoRA、RLHF、DPO 可直接用。

## 图像／视频／音频生成一句话

- 主流 = 文本编码器 + latent 上的 diffusion／rectified flow + Transformer 去噪网络；视频多一维时间；条件可换成音频、首帧、相机位姿。
- 自回归做图：先把图压成离散 token 再逐 token 生成。

## 陷阱

- "多模态 LLM 只靠文本训练""只处理结构化数据"错；"ViT 比 CNN 需要更少数据""ViT 只做分类"错。
- CLIP 测试不必同时用两个编码器。
- LLaVA 不更新视觉编码器。

## 讲义出处

- 图解第二页（flow matching、CFG、LDM、序列模型比较、VLA）：[cheatsheet/图解/流匹配CFG与LDM.html](../图解/流匹配CFG与LDM.html)，在线版 https://claude.ai/artifact/HznhhD5AMX36Qsguarpu5G
- 图解（六张示意图）：[cheatsheet/图解/diffusion与多模态.html](../图解/diffusion与多模态.html)，在线版 https://claude.ai/artifact/QCcaEWea7k6izudjB3yrpa
- ViT 结构：[Lecture 6 第 40–49 页](https://cqf.io/ARIN5203/lectures/Lecture6.pdf#page=40)；数据量比较：[第 53–57 页](https://cqf.io/ARIN5203/lectures/Lecture6.pdf#page=53)
- 多模态定义与三件套：[Lecture 11 第 3 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=3)、[第 9–10 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=9)
- CLIP：[第 11–12 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=11)；Flamingo：[第 13 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=13)；LLaVA：[第 15 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=15)；挑战：[第 20 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=20)
- VLA 定义：[第 31 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=31)；分层 vs 端到端：[第 36–37 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=36)；RT-2：[第 49 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=49)；RT-2 vs OpenVLA：[第 57 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=57)
- 文生图／视频：[Lecture 12 第 64–71 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=64)；自回归做图：[第 86–87 页](https://cqf.io/ARIN5203/lectures/Lecture12.pdf#page=86)
