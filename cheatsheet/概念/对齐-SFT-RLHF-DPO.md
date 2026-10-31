# 概念卡 · 对齐三步：SFT（instruction tuning）、RLHF、DPO

**触发：** 题干出现 alignment、instruction fine-tuning／tuning、RLHF、reward model、human feedback、preference、PPO、DPO。**讲义无专页**（Lecture 11 第 60 页只提到名字），考场查不到，靠这张卡。

## 小明例子

预训练模型 = 读过全世界的书但没接过客的新员工。

| 步 | 给他什么 | 要 reward model？ | 要 RL？ | 学会什么 |
|---|---|---|---|---|
| **SFT／instruction tuning** | 1 万张（指令，理想回答）卡片，有监督微调 | 否 | 否 | 看到指令就按格式答；适应特定数据，**保留通用能力** |
| **RLHF** | 同一问题两个回答，人勾"A 比 B 好"（成对偏好）→ 用这些数据**训一个评委（reward model）**打分 → 用 RL（PPO）让模型拿高分，加 KL 不偏离太远 | **是** | 是 | 两个都像人写的回答里哪个更好 |
| **DPO** | 同样的成对偏好（preferred vs not，**二元**）→ 跳过评委，直接训模型：拉高 preferred 的概率、压低 not preferred 的概率 | **否** | 否 | 同上，流程更简单稳定 |

## 每个名词一句话

- **Reward model**：用人类偏好数据**学出来**的模型，输入（问题，回答）输出分数，**预测人类偏好**。不是随机、不是手写规则、不限于仿真环境。
- **Instruction tuning 的目的**：让模型适应特定数据集／指令格式，同时保持通用能力。不是缩小模型、不是不要数据、不是只服务单一任务。
- **DPO 的好处**：去掉 reward model 和 RL 循环，训练简化。不保证所有场景最优；不是"比有监督学习数据更少"；不是"给 DPO 训 reward function"。
- **DPO 的反馈形式**：二元偏好。不是数值打分、不是连续反馈、不是文字评语。
- **"对齐"两个意思**：RLHF／DPO 对齐人类偏好；CLIP／LLaVA 第一阶段是图文**向量空间**对齐，与 RLHF 无关。

## 陷阱

- "reward model 是人工规则""DPO 需要 reward model""DPO 保证最优"都错。
- RLHF 和 DPO 用的数据同一种（成对偏好），差在要不要评委。
- 这些技术通用，可直接用于 VLA（Lecture 11 第 60 页）。

## 讲义出处

- 仅提及：[Lecture 11 第 60 页](https://cqf.io/ARIN5203/lectures/Lecture11.pdf#page=60)
- 课程大纲第 8 周列 alignment：[官方大纲](https://cqf.io/ARIN5203/about/syllabus.html)
- 第 5 天记录（小明例子）：[学习记录 · 第 5 天](../../arin5203学习记录.md)
