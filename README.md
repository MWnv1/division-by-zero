# 零可以做分母吗

**十四种自洽的形式化方案，以及每一种各自必须付出的那条公理。**

在线页面：`index.html`（单文件静态页，可直接部署到 Cloudflare Pages / GitHub Pages）

---

## 摘要

在通常算术里，`1/0` 与 `0/0` 不可能有值，这一点有严格证明，不是习惯问题。但在**改变某一条前提**的形式系统中，把 0 放在分母位不仅合法，而且有定理支撑、有完全公理化、有硬件实现、有千余年文献实践。

本文的主张不是"0 可以做分母"，而是一个更精确的命题：

> **0 可以做分母，当且仅当你愿意为它放弃一条公理。**

十四条方案，就是十四次不同的"交换"。任何声称证明了前者的论证，实际证明的都是后者。

---

## 1. 三条判据

一个表达式 `a/0` 要通过"可以做分母"的检验，需同时过三关：

| 判据 | 含义 |
|---|---|
| 语法 | 符号串在系统内是合法项，而不是被语法规则直接排除的写法 |
| 语义 | 它指称某个确定的对象（值），不是"未定义" |
| 理论 | 加入它之后系统一致，能推出该系统的定理，且限制到非零分母时与已知算术重合 |

下文所有方案的差别**只在第二关和第三关**，且它们不是"终于找到了方法"，而是"各自选择放弃一条公理"。

---

## 2. 不可能性定理：谁也绕不过的地基

**命题**[^1]：在任意满足 `0 ≠ 1`、加法与乘法构成交换幺半群、`0·0 = 0`、逆运算在非零元上给出真逆元的算术数据类型（premeadow）中，`0⁻¹` **不可能**是 0 的真乘法逆元，即恒有 `0·0⁻¹ ≠ 1`。

证明：

```
设 0·q = 1，则
  0 = 0·1 = 0·(0·q) = (0·0)·q = 0·q = 1
与非平凡假设 0 ≠ 1 矛盾。∎
```

这条命题的力度在于：它不是"数学家没找到办法"，而是**"找到办法"会与某条被放弃的公理冲突**。任何"0 做分母"的论证，本质都是在四条公理里挑一条来弃：

```
① 0·x = 0     ② x + (−x) = 0     ③ 1 ≠ 0     ④ 除法是全函数
```

---

## 3. 十四种方案

| # | 方案 | 1/0 | 0/0 | 放弃的那条公理 | 文献 |
|---|---|---|---|---|---|
| 1 | 平凡环 | 0 | 0 | `1 ≠ 0`（整个结构塌缩） | — |
| 2 | 对合 meadow | 0 | 0 | `x·x⁻¹ = 1` 无条件成立；UFAR 失效 | [2][3] |
| 3 | common meadow | ⊥ | ⊥ | `x + (−x) = 0` | [4] |
| 4 | 轮 wheel | ∞ | ⊥ | `0·x = 0`、分配律、`x/x = 1` | [5][1] |
| 5 | transreal | ±∞ | Φ | 与极限一致（改求值次序） | [6][1] |
| 6 | 黎曼球面 | ∞ | — | 域结构（∞ 非数） | [1][5] |
| 7 | IEEE 754 | ±∞ | NaN | 实数语义、结合律 | [7][8] |
| 8 | 三值逻辑 | 无值 | 无值 | 二值语义学 | [1] |
| 9 | 除法关系化 | ∅ | 全集 | 除法是函数 | [1] |
| 10 | 极限 / 不定式 | → ∞ | 待定 | 无（本来就允许） | — |
| 11 | 零微积分 | 0 | 0 | 与标准分析一致 | [11][12] |
| 12 | 条件期望 | 有值 | 有值 | 分母必须是数 | [13][14] |
| 13 | khahara（印度传统） | 无穷量 | — | 无 | [9][10] |
| 14 | Q₁ / Q₇₃₁ | 1 / 731 | 1 / 731 | 无（仅证明任意性） | [1] |

### 方案要点

**1｜平凡环**　令 `0 = 1`，则 0 的逆元就是它自己，`0/0 = 0` 完全合法。代价是整个数系退化为一个点。论证价值：**"0 可做分母"不是逻辑矛盾，只是要付出"整个结构消失"的代价**。

**2｜对合 meadow**　域签名上增加全函数逆运算，取 `0⁻¹ = 0`，于是 `1/0 = 0`。**唯一具备完全公理化地位的一条**。代价：`x·x⁻¹ = 1` 只在 `x ≠ 0` 时成立，无条件分数加法规则 UFAR 失效，只剩条件版 CFAR。

**3｜common meadow**　`0⁻¹ = ⊥`，⊥ 吸收一切运算。有 basis theorem。代价：`⊥ + (−⊥) = ⊥ ≠ 0` 撞上 `x+(−x)=0`，但换来 UFAR 成立。工程直觉最强。

**8｜三值逻辑**　不造新数，只承认 `1/0` 是合法语法项但无指称。在 Bergstra 的四种策略里：部分函数逻辑、误差代数、无穷合取、短接求值。把"不能做分母"从**语法禁令**降级为**语义空缺**。

**9｜除法关系化**　把 `b = a/c` 理解为约束 `a = b·c`。`c = 0` 时：`a ≠ 0` 解集为 ∅（商不存在）；`a = 0` 解集为**全体元素**（商欠定）。`0/0` 不是"无意义"，而是"全解"。

**10｜极限**　`lim sin x / x = 1`，导数定义本身就是 0/0 型，L'Hôpital 处理的就是 0/0。不放弃任何公理，代价是**答案依赖于如何逼近**。

**12｜条件期望**　`P(A|B)` 在 `P(B) = 0` 时分母为零，但用条件期望可推广到零概率事件。代价：依赖额外结构（σ-代数、极限方式、度量、最大熵）——即 Borel–Kolmogorov 悖论。**分母为零时商依然存在，前提是分母携带"如何逼近"的信息。**

**13｜khahara**　Brahmagupta（598–668）：正负数除以零，是"以零为分母的分数"。Bhāskara II："此分数称为无穷量（khahara）"，并引入"**0 上的待定运算**"，认为 `a×0/0 ≠ 0/0` 而 `= a`——几乎就是"除法是关系、需要上下文"的雏形。

---

## 4. 最强论证：把 `1/0 = 0` 写成定理

设签名 `Σ_md = ⟨0, 1, +, ·, −, ⁻¹⟩`，公理集 `Md` 包含：

```
(x⁻¹)⁻¹ = x + 0·x⁻¹        x·x⁻¹ = 1 + 0·x⁻¹
(x·y)⁻¹ = x⁻¹·y⁻¹          1⁻¹ = 1
0⁻¹ = 0                    0·(x·y) = 0·(x+y)
```

关键设计：不否认矛盾，而用"异常项 `0·x⁻¹`"把矛盾**吸收**掉，使 `0⁻¹ = 0` 与其余公理相容。

**定理（Bergstra–Tucker）**：`Md + C₀` 是特征 0 对合消去 meadow 等式理论的**有限完全公理化**；`Q₀` 是其初始代数。

论证三步：

1. **有值**：在 `Q₀` 中，`1/0` 是一个项的值，即 0。
2. **唯一**：该值由公理决定，不由人挑；不是约定，而是可判定的理论后果。
3. **可退化**：限制到 `x ≠ 0` 时退化为通常域运算，已知算术不被推翻。

代价精确地写在公理表上——`x·x⁻¹ = 1` 被换成了 `x·x⁻¹ = 1 + 0·x⁻¹`。

---

## 5. 轮式代数：最彻底的一条

Carlström 把除法做成**永远有定义**：`1/0 = ∞`，`0/0 = ⊥`，并证明**任意交换环或半环都可嵌入一个 wheel**——一条真正的嵌入定理，而不是约定。几何来源是"射影直线再加一个点 ⊥"，术语 wheel 取自拓扑图形 ⊙。代价最狠：`0·x = 0` 失效，乘法对加法不再分配，`x/x ≠ 1`。

工程变体：transreal 算术 `1/0 = +∞`、`−1/0 = −∞`、`0/0 = Φ`（nullity），43 条重写规则，合流且终止。代价：依赖"由内向外"求值次序。

只加一个 ∞ 的版本（黎曼球面）：`z ↦ 1/z` 在球面上是**连续映射**，0 是单极点。代价：∞ 不是数，`∞·0`、`∞−∞` 无定义。

IEEE 754：`3.0/0.0 = +Inf`、`−1.0/0.0 = −Inf`、`0.0/0.0 = NaN`。官方解释文件给出的语义理由是：非零数除以零"应被理解为分母小到不可表示时的比值极限，故最好用相应符号的无穷表示"。

---

## 6. 反方最强一击

Bergstra 构造：

```
P(x, y) = 1 / ( 1/x − 1/y )
```

在 `Q∞` 中 `P(0,0) = 0`；但沿路径 `x = y(1+x)` 让 `x, y ↓ 0`，得到 `P → 1`，故二重极限根本不存在。同理 `Q(x,y) = 1/((1/x)·(1/(1/y)))` 得 0 而极限为 ∞。

**所以：这些代数赋值不是极限的忠实记录。** 它们的"语义正当性"只能建立在"由内向外求值"这个**语法策略**上。

更能说明问题的是，Bergstra 在同一框架里构造了 `0⁻¹ = 1`（`Q₁`）与 `0⁻¹ = 731`（`Q₇₃₁`），后者的用意是：只要 731 不进入任何定理，它与 `1/0 = 0` 在理论上**同权**。

> 在 premeadow 框架内，`1/0` 取什么值，原则上不可被数学约束。

因此精确的结论是：**存在一个自洽的算术数据类型，其中 0 处于分母位且有值**——而不是"在通常算术里 0/0、1/0 有值"。前者可证，后者可证伪。

---

## 7. 结论与选型

> **0 可以做分母；代价是那个商不再是数，而是你选定的代数给出的一个标签——而一旦选定这个标签，你就必须交出使商唯一的那条公理。**

| 场景 | 用哪一条 | 理由 |
|---|---|---|
| 工程 / 硬件 | IEEE 754 | 标准强制，可复现，无需自建理论 |
| 证明助手 / 形式化 | 对合 meadow（`1/0 = 0`） | 有限完全公理化，可判定，其他点与域运算重合 |
| 几何 / 复分析 | 球面或 wheel | ∞ 与 ⊥ 有确定的拓扑含义（单极点） |
| 概率 / 统计 | 条件期望 | 分母是测度而非数，额外结构可消除歧义 |
| 教学 / 论证 | 平凡环 + khahara | 演示"逻辑上并非不可能，只是要付账" |

反过来，如果你要的是**唯一且可代换的商**，那么 0 必须留在分母之外——这不是禁忌，而是一条明确的定价。

---

## 参考文献

1. Bergstra, J. A. *Division by Zero: A Survey of Options*. 2019. —— [pdf](https://pdfs.semanticscholar.org/15d8/d647feee120dbc50e5247903ecc941429913.pdf)
2. Bergstra, J. A.; Bethke, I.; Ponse, A. *Cancellation Meadows: a Generic Basis Theorem and Some Applications*. arXiv:0803.3969. —— [pdf](https://arxiv.org/pdf/0803.3969)
3. Bergstra, J. A.; Tucker, J. V. *The Rational Numbers as an Abstract Data Type*. Journal of the ACM 54(2), 2007.
4. Bergstra, J. A.; Ponse, A. *Division by Zero in Common Meadows*. arXiv:1406.6878. —— [pdf](https://arxiv.org/pdf/1406.6878v1)
5. Carlström, J. *Wheels — on Division by Zero*. 2001/2004. —— [综述](https://handwiki.org/wiki/Wheel_theory)
6. Anderson, J. A. D. W.; Völker, N.; Adams, A. A. *Perspex Machine VIII: Axioms of Transreal Arithmetic*. Proc. SPIE 6499, 2007. —— [pdf](https://zenodo.org/record/810883/files/PerspexMachineVIII.pdf)
7. IEEE. *Standards Interpretation for IEEE Std 754-1985*. —— [pdf](https://standards.ieee.org/content/dam/ieee-standards/standards/web/documents/interpretations/754-1985_interp.pdf)
8. Kahan, W. *Lecture Notes on the Status of IEEE Standard 754*. —— [pdf](https://people.eecs.berkeley.edu/~wkahan/ieee754status/IEEE754.PDF)
9. O'Connor, J. J.; Robertson, E. F. *Bhaskara II (1114–1185)*. MacTutor. —— [链接](https://mathshistory.st-andrews.ac.uk/Biographies/Bhaskara_II/)
10. *Mathematics in India*（Bhāvanā）／印度统计研究所〈Zero〉专题. —— [链接](https://www.isid.ac.in/~rahul/zero/node3.html)
11. Okumura, H.; Saitoh, S. *Wasan Geometry and Division by Zero Calculus*. Sangaku J. Math. 2 (2018). —— [pdf](https://sangaku-journal.eu/2018/SJM_2018_57-73_okumura_saitoh.pdf)
12. Pinelas, S.; Saitoh, S. *Division by Zero Calculus and Differential Equations*. Springer Proc. Math. & Stat. 230. —— [链接](https://link.springer.com/chapter/10.1007/978-3-319-75647-9_33)
13. Gyenis, Z.; Rédei, M. *Conditioning Using Conditional Expectations: The Borel–Kolmogorov Paradox*. Synthese. —— [pdf](https://hps.elte.hu/~gszabo/Preprints/Borel-Kolmogorov.pdf)
14. HandWiki. *Conditioning (probability)*. —— [链接](https://handwiki.org/wiki/Conditioning_(probability))
15. *History of the Division by Zero and Division by Zero Calculus*. Roman Science Publications, 2022. —— [pdf](https://romanpub.com/resources/1.%20dbzc%202022.pdf)

## 诚实标注

零微积分（方案 11）在主流数学界**未被接受**；其"发现于 2014 年"的优先权主张被 Bergstra 用 1975 年 Komori 的文献直接反驳。transreal 算术同样不是标准算术的替代品。本文把它们列入，是为了完整呈现"自洽"与"被承认"之间的差别，而不是为其背书。

## 许可

本文为原创整理与论证，引用文献版权归原作者。转载或引用请注明出处与本文链接。
