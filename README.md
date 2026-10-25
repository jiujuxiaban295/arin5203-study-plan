# ARIN5203 复习资料

按 **2026 年 11 月 2 日考试、目标 70/100** 安排复习：[每日复习计划](arin5203复习计划.md)。考试日期来自个人提供的信息；考试范围为 **Lecture 1–12 与 10/26 课堂内容**。Lecture 1 写明期中考试在课上进行，预计周一 19:00 开考，**准确开考时间及开卷规则以老师通知为准**；2025 年试卷只用于参考题型与训练方法。

资料来源是 Canvas 课程公告链接的[教师公开课程网站](https://cqf.io/ARIN5203/)，目录核对日期为 **2026-10-25**。以下索引包含 12 份讲义、2 份数学补充、6 份历年试卷／答案和 3 份作业附件，共 **23 个文件**。本次仅整理原始资料及入口，没有新增题目、解答或学习笔记。

原始附件保存在[本仓库的 Releases](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/tag/course-materials-2026-10-25)，下表中的文件名均可直接下载。Git 仓库主分支保存复习计划、索引和校验清单。

## 每天先打开哪些资料

具体时长和完成标准见[每日复习计划](arin5203复习计划.md)，下表只映射已有资料。

| 日期 | 建议先读／练习 |
|---|---|
| 10/26 周一 | Lecture 1–2；两份数学补充按需查阅；2025 试题 Q3、Q2.5；晚上上课（内容计入考试） |
| 10/27 周二 | Lecture 5；2025 试题 Q1.6、Q2.3–4；Assignment 1 表 1 |
| 10/28 周三 | Lecture 3–4、6；2025 试题 Q2.1、6、7、10 |
| 10/29 周四 | Lecture 7–8；2025 试题 Q1.5、9、Q2.2、8 |
| 10/30 周五 | Lecture 9–12，并回看 Lecture 8；10/26 课堂讲义；2025 年计入范围的多选题 |
| 10/31 周六 | Lecture 4–5、8；数学补充；2025 Q3、Q2.5；2022 Q2.1、Q2.2、Q3(a)(d)；10/26 课堂讲义 |
| 11/1 周日 | 2021／2022 范围内未做过的题限时模拟 → 官方答案订正 → 对应讲义补弱项 → 2025 试卷复测 |
| 11/2 周一 | 已做错题、公式和对应讲义；最多 4 小时，17:30 前结束 |

今年讲义不含 RAG、NeRF／Gaussian Splatting 和 post-training 专讲；RLHF、DPO 等是否复习取决于 10/26 课堂内容，见计划中的“考试范围与旧题的对应”。资料索引本身不代表考试范围。作业附件用于按需回顾相关实践，不要求为了复习重新完成全部作业。先独立做题，再打开答案。

## 讲义（12 份）

官方目录：[Lecture Handouts](https://cqf.io/ARIN5203/lectures/index.html)。标题沿用目录；教师可能更新原站讲义。

| 文件 | 官方目录标题 | 官方来源 |
|---|---|---|
| [Lecture1.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture1.pdf) | Course introduction / Foundation model Preliminaries | [原文件](https://cqf.io/ARIN5203/lectures/Lecture1.pdf) |
| [Lecture2.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture2.pdf) | Introduction to Deep learning / Multilayer Perceptron | [原文件](https://cqf.io/ARIN5203/lectures/Lecture2.pdf) |
| [Lecture3.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture3.pdf) | Word2vec, RNN, LSTM | [原文件](https://cqf.io/ARIN5203/lectures/Lecture3.pdf) |
| [Lecture4.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture4.pdf) | Machine Translation, Attention, Transformer | [原文件](https://cqf.io/ARIN5203/lectures/Lecture4.pdf) |
| [Lecture5.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture5.pdf) | Convolutional Neural Networks | [原文件](https://cqf.io/ARIN5203/lectures/Lecture5.pdf) |
| [Lecture6.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture6.pdf) | Vision Transformer | [原文件](https://cqf.io/ARIN5203/lectures/Lecture6.pdf) |
| [Lecture7.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture7.pdf) | Generative Models: VAE, GAN | [原文件](https://cqf.io/ARIN5203/lectures/Lecture7.pdf) |
| [Lecture8.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture8.pdf) | Generative Models: Normalizing flow, Diffusion | [原文件](https://cqf.io/ARIN5203/lectures/Lecture8.pdf) |
| [Lecture9.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture9.pdf) | Generative Models: Flow Matching, Conditional Generation | [原文件](https://cqf.io/ARIN5203/lectures/Lecture9.pdf) |
| [Lecture10.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture10.pdf) | Pretraining | [原文件](https://cqf.io/ARIN5203/lectures/Lecture10.pdf) |
| [Lecture11.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture11.pdf) | Multimodal LLM and Vison-Language-Action Model (VLA) | [原文件](https://cqf.io/ARIN5203/lectures/Lecture11.pdf) |
| [Lecture12.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Lecture12.pdf) | Latent Diffusion Models | [原文件](https://cqf.io/ARIN5203/lectures/Lecture12.pdf) |

## 数学补充（2 份）

两份文件均由官方讲义目录直接链接。

| 文件 | 内容 | 官方来源／课程指定来源 |
|---|---|---|
| [MatrixCalculus.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/MatrixCalculus.pdf) | Matrix calculus | [原文件（University of Washington）](https://atmos.washington.edu/~dennis/MatrixCalculus.pdf) |
| [derivatives.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/derivatives.pdf) | derivatives notes | [原文件](https://cqf.io/ARIN5203/lectures/derivatives.pdf) |

## 历年试卷与答案（6 份）

| 文件 | 用途 | 官方来源 |
|---|---|---|
| [ARIN5203_Midterm_2025F_Problem.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/ARIN5203_Midterm_2025F_Problem.pdf) | 2025 试题；主要训练参考 | [原文件](https://cqf.io/ARIN5203/lectures/ARIN5203_Midterm_2025F_Problem.pdf) |
| [ARIN5203_Midterm_2025F_Solution.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/ARIN5203_Midterm_2025F_Solution.pdf) | 2025 官方答案 | [原文件](https://cqf.io/ARIN5203/lectures/ARIN5203_Midterm_2025F_Solution.pdf) |
| [COMP_5214_Midterm_2022S_Question.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/COMP_5214_Midterm_2022S_Question.pdf) | 课程提供的 2022 示例试卷 | [原文件](https://cqf.io/ARIN5203/lectures/COMP_5214_Midterm_2022S_Question.pdf) |
| [COMP_5214_Midterm_2022S_Answer.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/COMP_5214_Midterm_2022S_Answer.pdf) | 2022 示例答案 | [原文件](https://cqf.io/ARIN5203/lectures/COMP_5214_Midterm_2022S_Answer.pdf) |
| [Midterm_2021S.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Midterm_2021S.pdf) | 课程提供的 2021 示例试卷 | [原文件](https://cqf.io/ARIN5203/lectures/Midterm_2021S.pdf) |
| [Midterm_2021S_Solution.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Midterm_2021S_Solution.pdf) | 2021 示例答案 | [原文件](https://cqf.io/ARIN5203/lectures/Midterm_2021S_Solution.pdf) |

## 作业附件（3 份）

官方目录：[Programming Assignments](https://cqf.io/ARIN5203/programs/index.html)。此处保留公开发布的题目与原始代码包，不含个人提交或新编作业答案。

| 文件 | 内容 | 官方来源 |
|---|---|---|
| [Assignment1_2026F.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Assignment1_2026F.pdf) | Assignment 1 | [原文件](https://cqf.io/ARIN5203/programs/Assignment1_2026F.pdf) |
| [Assignment2.pdf](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Assignment2.pdf) | Assignment 2 | [原文件](https://cqf.io/ARIN5203/programs/Assignment2.pdf) |
| [Assignment2_code.zip](https://github.com/jiujuxiaban295/arin5203-study-plan/releases/download/course-materials-2026-10-25/Assignment2_code.zip) | Assignment 2 官方原始代码包 | [原文件](https://cqf.io/ARIN5203/programs/Assignment2_code.zip) |

## 录播与选读链接

- [Canvas 课程 Pages／录播入口](https://canvas.ust.hk/courses/71916/pages)：检查的 10 月 5 日录播显示 **Sign in required**，录播未下载，需在 Canvas 使用学校账号观看。
- [Matrix Calculus 交互工具](http://www.matrixcalculus.org/)：按需核对矩阵求导。
- [TensorFlow Neural Network Playground](https://playground.tensorflow.org/)：交互理解神经网络。
- [作业环境教程：Google Colab 与 PyTorch（YouTube）](https://www.youtube.com/watch?v=GooQPDMH2Uk)：课程作业页指定的环境教程。

以上交互网站和视频仅保留入口；未抓取完整外链教材、论文或额外模型／数据下载。官方 Assignment 2 压缩包内部自带文件保持原样。

## 来源与文件记录

原始附件未作内容修改，版权归原作者及相应权利人。本仓库未为第三方课程材料添加新的许可证；原文件中的作者署名、版权及使用说明继续适用。

[课程首页](https://cqf.io/ARIN5203/)的用途说明为：“All the materials are strictly for educational and non-profit purposes.” 本资料包用于学习复习，保留该教育及非营利用途说明。

[materials/manifest.json](materials/manifest.json) 记录每个文件的原始来源、获取时间、大小与 SHA-256，便于核对版本和完整性。
