# 概念卡 · 微调 vs ICL vs RAG；scaling laws 口径

**触发：** 题干出现 retrieval、RAG、retrieval-augmented、hallucination、knowledge update、prompt、few-shot、fine-tune 的取舍，或 scaling law。RAG **讲义无专页**，靠这张卡。

## RAG 三步

```
检索   retriever 把问题和文档都变向量，从文档库找最相似的几段
拼接   把找到的段落放进 prompt
生成   LLM 看着段落作答
```

四个好处：**知识随时更新**（换文档库）、**减少幻觉**（有材料可依）、**可溯源**（指出来源段落）、**不改模型参数**。

## 三方对比

| | 改参数？ | 需要梯度？ | 塞进 prompt 的是 | 解决什么 | 选它的场景 |
|---|---|---|---|---|---|
| 微调（含 SFT） | 是 | 是 | 无 | 学格式、风格、固定技能 | 固定输出 JSON 格式；长期任务 |
| ICL | 否 | 否 | 几个**任务示例** | 临时指定任务 | 临时给 3 个例子做翻译 |
| RAG | 否 | 否 | 检索到的**事实段落** | 模型不知道、会变的知识 | 每天更新的内部文档问答 |

## Scaling laws 口径

- 规律：模型越大、数据越多，困惑度可预测地下降；小模型实验可预测大模型。
- 成本 ∝ 参数 × token。预算固定时参数翻倍 → token 减半。
- 70B 配更多 token 胜过 175B：**参数与数据要配平**；"越大一定越好、与数据无关"错；"成本只和参数有关"错。
- 它是经验观察，不是定理。

## 陷阱

- RAG 不训练模型；"RAG 需要重训"错。
- ICL 和 RAG 都不改参数，区别是放示例还是放事实。
- 微调把知识固化在参数里，知识一变就要重训。

## 讲义出处

- Scaling：[Lecture 10 第 58–61 页](https://cqf.io/ARIN5203/lectures/Lecture10.pdf#page=58)
- ICL：[Lecture 10 第 53–57 页](https://cqf.io/ARIN5203/lectures/Lecture10.pdf#page=53)
- RAG：讲义无；大纲第 8 周列出：[官方大纲](https://cqf.io/ARIN5203/about/syllabus.html)
