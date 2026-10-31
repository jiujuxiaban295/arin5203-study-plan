# 计算卡 · Attention 复杂度、参数量、形状链

**触发：** 题干出现 self-attention、multi-head、sequence length n、embedding dimension d、heads h、time complexity、number of parameters、weight matrix (d, d/h)。

## 步骤

1. 抄下 n、d、h、d/h 四个数（别按习惯用 64）。
2. 判断口径：**包含投影**（标准）还是**已给 Q/K/V**（只剩分数和加权）。
3. 复杂度看 n，参数量不看 n。

## 形状链（包含投影）

```
X (n×d) → XQ、XK、XV (n×d) → 分数矩阵 QKᵀ (n×n) → softmax 加权求和 (n×d) → ·Y 输出投影 (n×d)
每头：X (n×d) · Q_i (d×d/h) → (n×d/h)；h 个头拼接回 (n×d)
缩放：分数除以 √(d/h)，防止点积过大、softmax 变 one-hot
```

## 公式

```
复杂度   O(n²d + nd²)     n²d 来自分数矩阵和加权求和，nd² 来自三次投影；h 约掉
         只给 Q/K/V → O(n²d)（没有投影步）；题目说 n ≫ d → O(n²d)（nd² 被压倒）
参数量   Q、K、V：3 · d · (d/h) · h = 3d²     加输出投影 Y：4d²     与 n 无关，h 约掉
         含 bias：每个投影加 d 个，Q、K、V、Y 共 4d
         题目只说 weight matrix 不加 bias，答时注明 excluding biases
```

## 例

- n = 10，d = 512，h = 8，每头 (512, 64)：Q、K、V 每头 3·512·64 = 98 304，8 头 786 432 = 3·512²；加 Y 1 048 576。
- d = 768，h = 12：3d² = 1 769 472；4d² = 2 359 296；再加 bias 4d = 3 072 → 2 362 368。
- d = 512：n = 1000 时 n²d = 5.12×10⁸ ≫ nd² = 2.6×10⁸；n = 10 时 nd² 主导；n = d 时相等。
- 反向：d = 256、每头 32、Q/K/V 共 393 216 → 3·256·32·h = 393 216 → h = 16。

## 陷阱

- 整理形状链漏写 n×n 分数矩阵，它是 n²d 的来源。
- "已给 Q/K/V 答 O(n²d)" 和 "n ≫ d 答 O(n²d)" 结论同、理由不同，写理由时别混。
- ViT 分数矩阵算不算 class token：196² 还是 197²，看题目有没有提。

## 讲义出处

- Q/K/V 三步与 softmax：[Lecture 4 第 35 页](https://cqf.io/ARIN5203/lectures/Lecture4.pdf#page=35)、[第 40–44 页](https://cqf.io/ARIN5203/lectures/Lecture4.pdf#page=40)
- Multi-head、缩放：[Lecture 4 第 58–61 页](https://cqf.io/ARIN5203/lectures/Lecture4.pdf#page=58)
- 复杂度 O(n²d)（只数分数矩阵）：[Lecture 4 第 77 页](https://cqf.io/ARIN5203/lectures/Lecture4.pdf#page=77)
- ViT 分数矩阵：[Lecture 6 第 49 页](https://cqf.io/ARIN5203/lectures/Lecture6.pdf#page=49)
- 详细推导：[第 3 天执行表](../../每日计划/第3天-Attention标准计算与位置编码.md)
