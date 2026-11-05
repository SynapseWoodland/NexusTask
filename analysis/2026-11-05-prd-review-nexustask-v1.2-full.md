# PRD 深度复评报告：NexusTask v1.2（文件 `PRD-nexustask-v1.0-full.md`）

- 评审日期：2026-11-05
- 评审对象：`docs/PRD-nexustask-v1.0-full.md`（文档内部版本 **v1.2**，见 [L18](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L18)；文件名与内部版本号不一致，见 P2-4）
- 上轮基线：`analysis/2026-11-05-prd-review-nexustask-v0.1.md`（v0.1 = 4.4/10，不合格）
- 作者自辩：`analysis/2026-11-05-prd-review-rebuttal-solo-ai.md`（承认 D1–D6，给出 8 项行动清单）
- 评审依据：prd-reviewer skill 内置评分体系 v1.0
- 交叉验证：`analysis/2026-11-05-effort-estimate-12h-ai.md`、`docs/PRD-nexustask-v0.4-converged.md`（仓库内均存在，已核对）

---

## 一、结论摘要

| 项 | v0.1 | **v1.2** | 变化 |
|---|---|---|---|
| 总分 | 4.4 / 10 | **5.8 / 10** | +1.4 |
| 评级 | 不合格 | **不合格**（距"待改进"差 0.2 分） | — |
| 上轮 D1–D6 设计洞 | 6 个全开 | **3 个已闭环、1 个部分闭环、2 个未闭环** | 详见 §三 |

**v1.2 是一份质量跃升的文档**：模板元信息、状态机、埋点、灰度、报表、验收标准全部补齐，FR 采用「需求描述 / 交互流程 / 页面元素 / 异常处理 / 埋点需求 / 验收标准」六段式，交互与产品逻辑的完备度显著高于基线。

**但它仍有 8 个会致命的 P0**。其中 3 个是 v0.1 时代就在、v1.2 换了个说法但没解决的；5 个是 v1.2 新写法引入的新矛盾。**最严重的一个动的是北极星指标本身**——D 档 12 道拒答题被算进了"结果集一致"口径的成功率分母里。

---

## 二、评分表（对比 v0.1）

| # | 模块 | 标准分 | v0.1 | **v1.2** | 得分率 | 本轮主要失分原因 |
|---|---|---|---|---|---|---|
| 1 | 基础信息完整性 | 1.0 | 0.0 | **0.0** | 0% | 扣分由 2.0 降至 1.3，但仍未触底：设计师/测试主R/需求提出人无位置，作者/评审人/负责人为"待确认"，日历日期待回填 |
| 2 | 项目/需求背景 | 1.5 | 0.1 | **0.2** | 13% | 业务场景、竞品、用户调研章节已补；仍缺业务侧量化数据，且北极星指标与业务价值之间无因果链 |
| 3 | 目标和收益 | 2.0 | 1.3 | **1.4** | 70% | 量化目标密集可判定；达成路径末尾 75%→80% 无排期；评估方式有两套复跑口径不一致 |
| 4 | 项目/需求详述 | 3.0 | 2.2 | **2.5** | 83% | 六段式 FR 完备；3 处状态机/事件表内部矛盾；全局埋点表漏 ~10 个 FR 内声明事件；无业务用户使用路径 |
| 5 | 灰度方案 | 0.5 | 0.3 | **0.5** | 100% | **满分**：明确"无需线上灰度/ABTest" + 替代机制 + 回滚判据（[L1603](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1603)、[L1431](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1431)） |
| 6 | 数据报表需求 | 0.5 | 0.2 | **0.4** | 80% | 字段+统计口径+展示形式齐全；归因看板口径与 FR-11 页面元素表述不一致 |
| 7 | 风险/合规披露 | 1.5 | 0.3 | **0.8** | 53% | §11.4 + §15 合规表已补；资金风险未用"跟钱相关/资金损失"框架；数据出境与供应商条款仍缺；无风控沟通结论 |
| | **合计** | **10.0** | **4.4** | **5.8** | **58%** | **不合格** |

**评分说明**：v1.2 已按 PRD 模板重写（变更日志 [L37](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L37) 自述"按 PRD 模板全量重写"），模板上限 6 分的红线未成为约束（5.8 < 6.0）。模块 1 归零仍属"模板税"，按作者自辩口径折算，内容分约 **6.8–7.0**（即模板税约 1.0–1.2 分，详见 §六）。

---

## 三、上轮 D1–D6 闭环情况核对

| 编号 | 上轮问题 | 闭环状态 | 依据 |
|---|---|---|---|
| **D1** | "成功率"未定义 | ⚠️ **部分闭环** | 已定义为"结果集一致"（[L1367](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1367)、[L1527](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1527)、比对规则 [L1038-1040](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1038)）。**但分母口径与 D 档拒答题冲突 → 见 P0-1** |
| **D2** | FR-06"与历史值比对"不可执行 | ✅ **已闭环** | 改为 `metric_profile`（指标×维度×月的 P5/P95/均值/σ，[L54](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L54)）+ 冷启动跳过并标 `no_baseline`（[L691](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L691)）+ 重算上限 1 次（[L725](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L725)） |
| **D3** | 口径歧义自相矛盾 | ✅ **已闭环** | `metric_kb` 每指标 ≥2 候选（[L562](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L562)）+ 五级消歧（[L57](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L57)）+ 物理锚点表（[L177-185](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L177)）+ 口径字典（[L189-196](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L189)） |
| **D4** | 状态机缺 CANCELLED / PARTIAL | ✅ **已闭环（但引入新矛盾）** | 10 态 + 20 条转移表（[L316-342](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L316)）。**但 REPLANNING 的目标态在三处不一致 → P1-5** |
| **D5** | 降级清单第一项砍四工作流 | ✅ **已闭环** | 14.1 明确"不可砍清单：状态机、Critic、评测对比表、失败归因"（[L1586](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1586)），四工作流在 [L256](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L256) 标注"不可砍（对比表是王牌）" |
| **D6** | 威胁模型错位 | ⚠️ **部分闭环** | 已改 AST 节点白名单 + 只读账号双边界（[L975-983](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L975)），并明确"正则不作为安全边界"。**但数据出境/供应商条款仍缺 → P1-11；输入侧无脱敏 → P2-9** |
| **工期前提**（P0-4） | 6 周 × 2–3h 与 15–17 天 × 12h 冲突 | ✅ **已闭环** | 14.2 明确"30 个工作日 × 12h"（[L1597](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1597)），与自辩文件建议的"3 周 + 1 周缓冲 + 2 周理解预算"一致 |

**结论：作者诚实、自洽，且技术判断力比 v0.1 有明显提升。** 上轮 6 个设计洞解决 4 个。**但 v1.2 的新写法引入了另一批问题——它们大多不是"缺失"，而是"两处条款互相打架"，恰恰是评审最难在 5 分钟内发现、面试现场最容易被问穿的类型。**

---

## 四、新发现的问题

### P0 级（阻断级：不改会在面试现场被问穿，或让核心数字不可信）

---

#### P0-1｜北极星指标的分母把 D 档拒答题算进了"结果集一致"口径 —— **动的是北极星本身**

- 13.2 效果指标表 [L1527](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1527)：
  > 任务成功率 = **结果集一致任务数** / (总题数 − contested 数) ｜ 门限 ≥80% ｜ 北极星
- 9.2 分档门限表 [L1379](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1379)：
  > D 拒答与边界 ｜ **≥85%（拒答正确率）**
- 9.1 题库 [L1346](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1346)：50 题 = A12 / B12 / C14 / **D12**

D 档 12 题（越权、无数据、口径不可消解、超数据范围）**没有结果集可比**，其正确形态是"拒答且理由正确"。但北极星公式的分子是"结果集一致任务数"、分母是全部 50 题减去 contested。**两套判定标准被混进同一个分数**：D 档答对了却因为"无结果集"而不计入分子，等价于 12/50 = 24% 的天花板被凭空扣掉 → **北极星指标的可达上限实际是 76%**，而门限写的是 80%。

**这意味着 PRD 自定的北极星目标在定义上就不可达。** 面试官问"你成功率 80% 是怎么算的"，把公式和 D 档门限并排摊开，数字自相矛盾。

**修法**（三选一，推荐第 1）：
1. 公式改为 `任务成功率 = (A/B/C 档结果集一致任务数 + D 档拒答正确任务数) / (总题数 − contested 数)`，并在 13.2 增列"拒答正确率"为独立辅助指标；
2. 北极星分母改为 38（A+B+C），D 档单列"拒答正确率 ≥85%"作为并列硬门限，13.2 同步改写；
3. D 档从 50 题中抽出独立成 12 题的"拒答集"，北极星只在 38 题上定义。

---

#### P0-2｜"双人独立编写标准 SQL"在单人项目里没有人 —— **contested 机制事实上失效**

- 9.1 标准答案制定 [L1349](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1349)：
  > **双人独立编写** → 结果不一致的题进入争议池 → 复核后标记 corrected 或 contested
- 15 风险表 [L1613](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1613)：50 题标准答案有争议导致指标失真 → 应对 = 双人独立编写 + 争议池
- 14.1 里程碑表 [L1546-1552](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1546)：负责人列**全部为"待确认"**，全文只有一个人

**contested 池是防止"标准答案本身错 → 指标失真"的唯一防线，也是"禁止为提分滥标 contested"（[L1350](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1350)）的执行前提。单人写 50 题标准 SQL 必然带着自己写题时的口径偏好，标准答案和系统用同一套口径理解 → **两个"独立"实为同一个大脑，争议池永远不会触发**。

**修法**：把"双人"换成可执行的伪双盲，明确写进 9.1：
> **双盲 = LLM 起草（模型 A，temp=0，prompt 固定）→ 人独立复核（不看模型答案前先自己写一遍 SQL）→ 分歧进争议池 → 争议题由人裁决并记录裁决理由**。D16–D18 的 3 天按此排期，人只做"裁决分歧题"这一件事。
> 附：**第二标注者 = 不同厂商模型**（如 DeepSeek 起草、人用另一模型交叉），比同模型自比更接近真双盲。

---

#### P0-3｜checkpoint 粒度是状态级，验收要求却是节点级 —— FR-05 验收不可达

- 6.3.6 交互流程第 1 步 [L645](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L645)：
  > **每次状态迁移前写 checkpoint**（含任务态、已完成节点、预算余量）
- 6.3.6 验收第 1 条 [L675](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L675)：
  > 在执行**第 3 个节点**时 kill -9 进程，重启后任务**从第 4 个节点继续**，前 3 个节点不重复调用工具

按 [L645] 的写法，checkpoint 在**状态迁移**时写。EXECUTING 是一个状态，DAG 的 n1/n2/n3 全部发生在同一个状态内部，**状态级 checkpoint 在 n3 被杀时恢复到的仍是 EXECUTING 起点**，n1–n3 会被整体重跑。"从第 4 个节点继续"要求的是**节点级 checkpoint**，而 PRD 从未定义它。

**且"已完成节点"字段只是 checkpoint 的一个载荷**，不构成节点级持久化语义。这条验收按当前设计**必然失败**，而它是"容错能力"最直观的演示点。

**修法**：把 checkpoint 粒度明确为**节点级**：`每个 DAG 节点执行前后各写一次节点 checkpoint（含已完成节点集合 + 预算余量 + 节点输出引用）`，并把 [L645] 改为"每个节点执行前写节点级 checkpoint；状态迁移仅记状态日志（可由节点 checkpoint 推导，不单独持久化）"。同时在验收里补一句"节点输出以引用形式存 Redis/DB，不重放 LLM 调用"。

---

#### P0-4｜追问快路径的变更分类**漏掉了"换口径 / 换指标"——恰好是本项目的核心场景**

- 6.3.1 双路径表 [L401](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L401)：
  > 快路径：AST 差分 ｜ 触发条件 = 变更属于 **A 类（WHERE 字面量替换）、C 类（LIMIT / ORDER BY）、D 类（追加 WHERE 过滤）**
- 3.1 五级消歧 [L57](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L57)：口径歧义是本项目的立论核心
- 4.4 端到端示例 [L140](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L140)：第一步就是消歧

**"那按金额算呢"（换口径）、"那退款率呢"（换指标）是追问里最高频的两类，而分类表里没有对应类目。** 结果是这类追问 100% 落到主路径 rewrite —— 这本身不算错，但意味着：

1. **快路径的价值主张被削弱**：P2 的实验设计目标若是"证明确定性改写优于 LLM 编排"，而最需要优化的歧义场景又恰好进不去，实验结论无法推广；
2. **更严重的是口径切换与维度切换叠加时无解**："那按金额算的华东呢" = 换口径（A/B/C/D 都不覆盖）+ 换维度（D 类勉强覆盖追加 WHERE）—— 分类表给不出答案；
3. FR-01 验收 [L458](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L458) 只测 A/C/D 三类改写与主路径一致率 ≥95%，**绕开了口径切换的正确性**，等于把最危险的一类排除在验收外。

**修法**：补 **G 类（换口径 / 换 `definition_id`）**，规则明确"口径变更一律走主路径 rewrite，仅当新旧 `definition_id` 的声明式定义除 measure/filters 外完全一致、且变更仅涉及该定义内的口径切换时才允许 AST 改写"；并在 FR-01 验收增加一条"口径切换类追问（≥4 题）必须正确定稿 `definition_id`，且最终 SQL 的 measure/filters 与所选口径定义逐字段一致"。

---

#### P0-5｜FR-08 内部自相矛盾：既要求"四模式分母完全相同"，又允许某模式"不参与成功率排名"

- 6.3.9 异常处理 [L788](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L788)：
  > 某模式超时率过高 ｜ **单独标注，不参与成功率排名**
- 6.3.9 验收第 2 条 [L800](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L800)：
  > **四种模式的成功率分母完全相同**（同一题库、同一 contested 剔除规则）
- 6.3.3 FR-03 异常处理 [L537](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L537)：SQL 超时 → 计入 `TOOL_EXEC`

**超时导致某模式被排除出排名 → 分母必然不同 → 违反自己的验收标准。** 更危险的是它给了一条"把表现差的模式踢出对比表"的合法路径 —— 而这张对比表是 FR-08 自认的"王牌"（[L256](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L256)），也是 JD 要求 3 的唯一应答素材。面试官问"某个模式为什么没进表"时，这个问题无法回答。

**修法**：删除"不参与成功率排名"，改为"**该模式单独标注超时率与超时任务占比，但成功率照常计入（超时任务计失败）**"；超时率另设辅助门限（如"单模式超时率 ≤10% 超标则该模式结果标注为不稳定"），不得剔除。

---

#### P0-6｜"标准 SQL 执行成功率 100%"与"执行失败标 contested"直接互斥

- 6.3.14 验收第 1 条 [L1081](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1081)：
  > 50 题全部可执行，**标准 SQL 执行成功率 100%**（contested 单独标注）
- 6.3.14 异常处理 [L1069](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1069)：
  > 标准 SQL 本身执行失败 ｜ 该题标 `contested`，**不进分母**，必须人工复核
- 9.1 [L1350](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1350)：contested 题从成功率分母剔除并单独报告数量

若标准 SQL 执行失败必然产生 contested，则"执行成功率 100%"与"存在 contested"不能同时为真。**这条验收按当前表述不可判定。**

**修法**：把两个概念分开并给出目标值：
> **标准 SQL 可执行率 = 100%（硬要求，50 题全部必须能跑出结果）**；**contested = 标准 SQL 可执行但口径本身存疑**（如"退款率按单还是按金额"在标准答案中仍有争议）。目标 contested 数 ≤3（≤6%），且逐条给出裁决理由。执行失败的标准 SQL 属**题库缺陷（bug）**，必须修题，不得记为 contested。

---

#### P0-7｜D25 门限 75% 与最终验收 80% 之间没有排期 —— 最后 5 天全是收尾

- 9.2 准确性 [L1367](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1367)：任务成功率 **≥80%**（D20 门限 60%，D25 门限 75%）
- 14.1 [L1579](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1579)：D25 门限 2 = **≥75%**
- 14.1 D26–D30 [L1580-1584](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1580)：K8s / 压测 / pgvector 降级 / README / 录屏 / 终评 / 简历回填 —— **无一天用于调优**
- 14.2 [L1597](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1597)：30 工作日 × 12h

**最后 5 天没有一天能用来从 75% 冲到 80%。** 若 D25 实测停在 75%，D30 的"简历数字回填"只能写 75%，而 §9.2 的验收标准是 80% —— **计划本身无法同时满足阶段门限和最终门限**。且上一轮工期估算已指出"调优到 80% 是最大不确定性、串行等待"，D21–D24 四天从 60% 提到 75%（日均 3.75 点）本身已偏紧。

**修法**：二选一并在 PRD 里写死
- **A（推荐）**：D26–D27 改为"调优窗口（预留 2 天，目标 75%→80%）"，K8s 降级为 D28 可选（14.3 已声明"无需线上灰度"，K8s 在 [L1586](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1586) 之外不是不可砍项）；
- **B**：把最终门限正式下调为 ≥75%，并把 80% 改为"加分目标"，同步修改 §9.2 与 14.1，别留一个不可达的硬指标。

---

#### P0-8｜评测本身的 LLM 调用量与 API 成本没有算进预算

- 6.3.14 零回归 [L1048](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1048)：单题判定取 **k=3 复跑**
- 9.2 稳定性 [L1369](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1369)：同题重复 **5 次**一致率
- 6.3.9 [L799](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L799)：50 题 × 4 模式 = 200 次运行
- 7.2.3 [L1189-1192](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1189)：单任务 5–8 次调用、30k–70k token、¥0.25–0.8/任务
- 10.4 [L1429](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1429)：**每次 prompt 改动必须附回归结果**

**算一遍**：一次完整门禁 = 50 题 × 4 模式 × 3 次复跑 ≈ **600 次任务运行**；叠加稳定性 5 次 ≈ 1000 次；每次任务 5–8 次 LLM 调用 → **单次全量门禁 ≈ 3000–8000 次 LLM 调用 ≈ ¥150–600**。而调优期 D21–D24 每天改 prompt，**每天一次门禁 = 4 天 ≈ ¥600–2400**。

PRD 只在 14.2 估了"时间 30 天 × 12h"，**API 费用这一栏完全缺失**。这不是小数 —— 它与"单任务成本 ≤¥0.5"是同一项指标的两个尺度，而 PRD 对后者门限很严、对前者只字未提。

**修法**：在 9.1 或 14.2 补一张「评测算力预算」表：

| 场景 | 运行次数 | 单次成本 | 小计 | 频次 |
|---|---|---|---|---|
| 首轮跑分（D19） | 50 × 4 = 200 | ¥0.3–0.8 | ¥60–160 | 1 次 |
| 门禁（k=3 复跑） | 600 | ¥0.3–0.8 | ¥180–480 | 每日（调优期 4 天） |
| 稳定性 5 次 | 1000 | ¥0.3–0.8 | ¥300–800 | 1 次 |
| **合计** | — | — | **¥540–1440** | — |

并写明降本手段（门禁期间关 rerank、只跑受影响题型子集做日常回归、k=3 只对变更相关题复跑）。

---

### P1 级（影响专业度与可执行性）

---

#### P1-1｜`fact_settlement` 的粒度与行数差 48 倍，净收入口径因此不可下钻

- 4.5 表定义 [L159](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L159)：粒度 = "**一个商家一天的结算单**"，行数 = **30,000**
- 4.5 维度 [L150](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L150)：`dim_merchant` = 2,000 个商家
- 4.5 时间基准 [L146](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L146)：24 个月

2,000 商家 × 24 月 × 30 天 = **1,440,000 行**，实际写 30,000 —— **差 48 倍**。这张表是 §4.5 口径字典第 2 个指标"净收入"的唯一来源（[L192](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L192)：`SUM(net_amount)`）。

更实质的问题：`fact_settlement` **没有 `order_id` / `refund_id` 外键**（对比 `fact_refund` 有 `order_id`+`payment_id`），只能靠 `merchant_id + settle_date` 聚合 → **净收入无法下钻到订单/退款层**，4.4 的 C 档归因题（"退款率为什么涨、哪些商家和品类贡献最大"）在净收入口径下**不可验证**。这是数据模型的设计缺口，不是行数笔误。

**修法**：① 明确结算粒度 —— 若按 `settle_cycle`（T+1/T+7）结算，则粒度是"商家 × 结算批次"，行数改为 ≈ 2,000 × 24 月 × 4 批次/月 ≈ 192,000，或改为"每商家每周一批"≈ 2,000 × 104 周 = 208,000；② 给 `fact_settlement` 增加 `settlement_item` 子表或至少 `refund_id` 关联列，使净收入可下钻；③ 若坚持 30,000 行，则必须把粒度改写为"商家 × 结算周期（月结）"并在口径字典中同步。

---

#### P1-2｜没有 `dim_date`/日历骨架，会让趋势与环比类题目算错

- 4.5 [L161](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L161)：
  > 合计约 56 万行。**没有 `dim_date`**：时间维度用事实表时间列 + `DATE_FORMAT` / `QUARTER()` 派生，**少一张表不影响问法覆盖**
- FR-03 `sql_query_trend` [L516](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L516)：时间粒度 ∈ {day, week, month}

**"少一张表不影响问法覆盖"这个判断是错的。** 时间序列用事实表 `GROUP BY DATE_FORMAT(...)` 生成，**某期无数据就没有那一行**（例如某品类某月零退款 → 缺行）。后果：① 趋势图断点，环比计算对不上期（缺行被当成 0 还是被跳过？两种都错）；② `sql_query_trend` 返回的序列与标准答案无法对齐，而 B/C 档的对比与归因题大量依赖环比 —— **这会直接压低北极星指标，且原因是数据模型而非 Agent 能力**。

**修法**：加回 `dim_date`（24 个月 ≈ 731 行，成本可忽略），或给出等效方案：在 `sql_query_trend` 渲染时用 `generate_series`/递归 CTE 生成连续日期轴再 LEFT JOIN 事实表。**两者选一，并写进 4.5 与 FR-03。**

---

#### P1-3｜退款链路的跨表金额不变量没有校验规则

- 4.5 合成规则 [L200-201](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L200)：恒等式校验只覆盖**订单头**（`goods − discount + freight + tax = payable`）；退款侧只写"退款金额 ≤ 对应支付金额"作为生成约束，**无全量校验**
- 4.5 [L158](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L158)：`fact_refund` 有 `payment_id` / `refund_amount` / `refund_status`
- 口径字典 [L193](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L193)：退款率 = `SUM(refund_amount) / SUM(pay_amount)`，两侧均取 `success`

退款率是 4 个核心指标之一，分子分母跨两张表，但**生成阶段没有"所有退款金额之和 ≤ 对应支付金额之和""同一订单退款总额 ≤ 其 paid_amount""退款状态流转不影响已计入的支付额"这类跨表不变量校验**。PRD 在订单头层面做到了"生成后跑一次全量恒等式校验，不通过即中止"（[L200](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L200)），**这个好做法没有延伸到退款链路**。

**修法**：在 4.5 合成规则补第二条全量校验：
> 退款链路校验（生成后全量跑，不通过即中止）：① 同一 `order_id` 的 `SUM(refund_amount) ≤ fact_order.paid_amount`；② `fact_refund.pay_amount` 口径下 `SUM(refund_amount) ≤ SUM(pay_amount)`；③ 每笔 `refund.payment_id` 必须存在于 `fact_payment` 且 `pay_status='success'`；④ 仅退款/退货退款的 `is_after_sale` 与 `refund_time` 相对 `order_time` 的天数分布满足口径字典中"售后期"的定义。

---

#### P1-4｜REPLANNING 的目标态在三处互相矛盾

- 6.1 状态转移表 #20 [L342](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L342)：**REPLANNING → PLANNING**
- 6.1 产品流程图 [L308](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L308)：[REPLANNING] ──▶ **重执行**（重算 ≤1）
- 8.4 链路图 [L1323-1326](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1323)：[⑥ 重规划 ≤1 次] → **[EXECUTING]**
- 6.3.8 FR-07 [L740](file:///D:/github/Nexustask/docs/PRD-nexustask-v1.0-full.md#L740)：REPAIR 时把「修复目标节点 + 动作 + 理由」结构化回传给 **Planner**

**两处画图说回 EXECUTING，状态表说回 PLANNING。** FR-07 支持"回 PLANNING"（回传给 Planner 重新生成），但"回 EXECUTING"也说得通（保留 DAG，仅重跑失败节点）。**两种语义完全不同**：回 PLANNING = 重新规划整张 DAG（节点数、依赖都可能变）；回 EXECUTING = 保留 DAG 只重跑指定节点（对应 Critic 的 `repair_action.target_node`）。FR-06 的 REPAIR 动作设计（[L697](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L697)）明显是后者。

面试现场"REPAIR 之后回到哪个状态、会不会重新生成整张 DAG"是必问题。

**修法**：统一为 **REPLANNING → EXECUTING（仅重跑 `repair_action.target_node` 及其下游）**，并把状态表 #20 改过来；同时明确"若 Critic 给不出合法 `target_node`，则退化为 REPLANNING → PLANNING 全量重规划"。两处图同步改。

---

#### P1-5｜`temperature=0 ⇒ 同一 run 可复现` 是技术断言错误，且与"5 次一致率 ≥90%"互相拆台

- 6.3.14 [L1046](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1046)：
  > 门禁跑分用 `temperature=0`，**同一 run 可复现**
- 9.2 稳定性 [L1369](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1369)：
  > **同题 5 次结果一致率 ≥90%**

temperature=0 **不等于**确定性输出：批处理、连续批处理算子、浮点非结合性、MoE 路由、服务端负载都会引入差异，主流厂商 API 在 temp=0 下仍不可复现是公开事实。

两个条款互相拆台：**若真的可复现，5 次一致率恒为 100%，90% 门限测不出任何东西**；若承认不确定（这是事实），那 [L1046] 的表述必须改，而 k=3 复跑 + 零回归的设计反而是对的、值得保留。

**修法**：
> [L1046] 改为"门禁跑分固定 `temperature=0` 以**降低**方差，但**不假定完全可复现**；同一 run 的结果差异记入 `run_variance` 字段"。9.2 的 5 次一致率门限保持（它正是用来量化这部分方差的），并把 k=3 复跑的设定与它对齐（同一题 5 次中 ≥3 次 FAIL 才计回归，与 [L1048] 的 k=3 ≥2 次 FAIL 口径统一为一条规则）。

---

#### P1-6｜幻觉率 ≤2% 的门限，样本量与判定方式都支撑不住

- 9.2 幻觉率 [L1370](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1370)：
  > 输出中每个数字与工具返回值做指纹比对；**结论文字中的因果断言是否引用了未出现的证据** ｜ **无依据数值占比 ≤2%**
- 11.3 抽查机制 [L1464](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1464)：
  > **每周人工抽查 10 条** COMPLETED 任务，核对数值与标准 SQL；发现 1 条幻觉即触发全量回归

两个问题：

1. **"结论文字中的因果断言是否引用了未出现的证据"是纯语义判断**，PRD 却在 9.2 给了 ≤2% 的硬门限。这个门限要么靠人工判（则每周 10 条的抽查量根本推不出 2%），要么靠 LLM 判（则需再定义"判定 LLM"及其自身误判率）。
2. **量级不自洽**：50 题 × 4 模式 = 200 次运行，"≤2%" = **最多 4 次**。而每周抽查 10 条要覆盖 200 次运行需要 20 周。**抽样量与门限差一个数量级**。
3. 另外，§11.3 的抽查是**事后**机制（"发现 1 条幻觉即触发全量回归"），而 9.2 的门限是**评测时**指标，两者的时间尺度不同，不能互相支撑。

**修法**：把 9.2 的幻觉率改为**两层**：
> **数值幻觉率（自动化，门限 ≤2%）**：仅统计"数字未出现在工具返回值中"，由数值指纹自动判定，可全自动门禁。
> **结论幻觉率（半自动，观测项不做门禁）**：因果断言的证据引用由人工抽检记录，**不设硬门限**，只报告抽检数与检出数；同时把 §11.3 的抽查量从"每周 10 条"改为"每次全量跑分后抽查 20 条（含全部 COMPLETED 的 4 类题型各 5 条）"。

---

#### P1-7｜L4 兜底丢掉 `depends_on`，直接破坏 FR-02 的拓扑序不变量

- 11.1 L4 [L1444](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1444)：
  > 仍失败 → 降级到简化 schema（**仅保留 node_id / tool / args**）
- 6.3.2 FR-02 验收第 3 条 [L502](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L502)：
  > 合法 DAG 的执行顺序**严格符合拓扑序**

简化 schema 去掉 `depends_on` → DAG 退化为一个无依赖的节点列表 → **执行顺序变成列表顺序，拓扑序不变量被兜底机制自己破坏**。而 L4 是"LLM 两次都输出不合规"后的保命路径，触发概率虽低但一旦触发，产出的是一个**看起来成功、实际错误的 DAG**。

**修法**：L4 保留 `depends_on`（它是 4 个字段里语义最关键的一个），只去掉 `expected_output` 与可选字段；并补一条"若 L4 产物仍不成环且节点数 ≤8，则进入 EXECUTING 并标记 `degraded_schema=true`；若成环 → L5 FAILED（failure_class=PLAN）"。

---

#### P1-8｜成本口径三处不一致：单费率 vs 输入/输出双单价、P95 样本集不一致

- 7.2.3 [L1192](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1192)：
  > 按**输入 ¥8–12 / 百万 token** 估算，单任务成本约 ¥0.25–0.8
- 13.2 [L1531](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1531)：
  > 单任务成本 = Σ（**输入 token × 单价 + 输出 token × 单价**）/ 任务数 ｜ P95 ≤ ¥0.5

两处矛盾：① 7.2.3 只用**一个**费率估算，但 13.2 的公式区分输入/输出，而主流厂商**输出单价通常是输入的 3–5 倍** —— 7.2.3 的 ¥0.25–0.8 系统性**低估**；② 6.3.11 FR-10 验收 [L912](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L912) 说"单任务成本 P95 ≤ ¥0.5（**50 题 × 4 模式**统计）"，13.2 的 P95 没限定样本集 —— **两个 P95 的样本集不同**（200 次混合 vs 单任务），混合 P95 会被最贵的 Multi-Agent 模式拉高，而单任务 P95 更接近 13.2 的定义。

**修法**：统一为"**分模式给门限**"：
> 成本门限按模式分别设定：FC / ReAct ≤¥0.25，P&E ≤¥0.35，Multi-Agent ≤¥0.6（Multi-Agent 天然最贵，不应与 FC 同门限）；13.2 的"单任务成本 P95"明确为**单模式内 P95**；7.2.3 的估算改为双费率（输入 ¥X/百万、输出 ¥Y/百万，Y ≈ 3–5X），并按 7.2.3 的 token 结构重算区间。

---

#### P1-9｜P95 < 10s 对追问子集不成立 —— 追问要多一次 LLM 调用

- 8.3 [L1273](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1273)：单任务 P95 延迟 < 10s（不含人工澄清等待）
- 6.3.1 主路径 [L400](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L400)：
  > 将「上一轮问句 + 已确认口径 + 上一轮 SQL 结构 + 本轮追问」**改写为一条自包含完整问句**，再走 FR-02 正常规划链路
- 7.2.3 [L1189](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1189)：单任务 5–8 次调用

追问 = **额外一次 rewrite 调用**（1–2s + 1.5–2k token）→ 端到端变成 6–9 次调用、12–20s 量级，**系统性超 10s 门限**。而 FR-08 恰好要求"同一道追问在基线与最优模式下的差异（**延迟**/成本/正确性）"（[L803](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L803)）—— 追问恰好是延迟最差的一类，被拿来对比的样本正好落在超门限区。

**修法**：把延迟门限**按题型分档**（与非功能需求表一致）：

| 题型 | P95 延迟门限 | 说明 |
|---|---|---|
| A / B（单轮） | < 10s | 现行门限 |
| C / 追问子集 | < 20s | 含 1 次 rewrite |
| 澄清等待 | 不计入 | 现行说明保留 |

并把 rewrite 的一次调用计入 7.2.3 的"单任务调用次数"（改为 5–9 次，追问类单列）。

---

#### P1-10｜架构图漏 `create_ticket`，且 D2 排期只做 5 个工具

- 8.4 链路图 ④ Executor 工具清单 [L1308-1313](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1308)：只列 6 个（`sql_query_metric` / `sql_query_dimension` / `sql_query_trend` / `sql_query_contribution` / `sandbox_calc` / `chart_render`）—— **漏了 `create_ticket`**
- 5.1 功能架构 [L232](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L232)："4 只读 SQL + sandbox + chart + **工单**" ✓ 7 个
- 6.3.3 FR-03 [L510](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L510)："7 个工具" ✓
- 14.1 D2 [L1559](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1559)："工具注册表 + **5 工具**" —— `chart_render` 与 `create_ticket` **没有排期日**
- 7.2.3 [L1184](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1184)："工具 schema（**7 个**）1.5k–2k" ✓

三处（架构图 / 排期 / 需求）互不一致，且 `create_ticket` 是 FR-12 安全设计中"唯一写入类操作"与 FR-14 幂等的演示载体，**没有它，幂等考点少一半**（4 个幂等接口里 3 个是幂等键去重）。

**修法**：8.4 链路图补 `create_ticket`；14.1 把 `chart_render` 排入 D10（随单页/图表）、`create_ticket` 排入 D14（随审计表），并在 D2 明确"D2 先做 4 只读 SQL + sandbox_calc 共 5 个，其余在对应里程碑补齐"。

---

#### P1-11｜合规仍缺：模型服务商数据出境/留存/训练条款，输入侧无脱敏

- 11.4 第三方 [L1476](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1476)：
  > LLM 调用外发内容仅含问句、口径定义、工具 schema 与结果摘要；**不含真实用户数据**
- 15 合规风险表 [L1620-1622](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1620)：资金相关 / 数据泄露 / SQL 注入三条

已闭环的部分做得好（合成数据、无 PII/无商标、AST + 只读账号双边界）。**未闭环的三条**：

1. **数据出境未评估**：即使无真实用户数据，"问句 + 结果摘要（含合成金额）"发往境外/境外厂商，属于数据出境范畴，PRD 全文未提地域、数据留存周期、是否被用于供应商训练。这在 §4.3 "不依赖任何商业产品未公开的能力"的严谨基调下是明显缺口。
2. **输入侧无脱敏**：11.4 只约束"出站内容"，**没有约束入站内容**。演示用户完全可能在问句里粘贴真实手机号/姓名/公司名，而这些会随问句外发。§11.4 无"输入侧过滤/脱敏"这一项。
3. **无风控/法务沟通结论**：rubric 要求"有风险需标注沟通结论"。作为非商业作品集，正确写法是"**不涉及真实业务与真实用户，不经手任何个人金融信息，故不触发法务/财务/风控流程**"，而不是留白。

**修法**：11.4 补两行 + §15 补一行：

> **数据出境**：默认使用境内厂商模型；若评测需对比境外模型，单独标注"合成数据出站，无真实个人信息"，并在 `decisions/` 记录该次出站的数据范围与所用供应商的留存/训练条款。
> **输入侧**：问句提交前经正则 + 长度校验，命中手机号/身份证/银行卡/邮箱模式时**前端提示并阻断**，不外发。
> **沟通结论**：本项目无真实用户、无真实资金、不经手个人金融信息，**不进入法务/财务/风控评审流程**；风险控制以代码层双边界（只读账号 + AST 白名单）承担。

---

#### P1-12｜FR-04 的验收分母依赖 P1 的 FR-04b，且"双路检索"在 D9 之前不存在

- 6.3.4 FR-04 验收 [L596](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L596)：
  > 拔掉 Milvus 后系统仍可完成 A 档题（单指标），**成功率不低于双路检索时的 70%**
- 5.2 [L252](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L252)：FR-04b RAG 优化 = **P1**
- 14.1 [L1566](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1566)：混合检索 + rerank 排在 **D9**

FR-04 是 P0，验收标准却以 P1 特性（双路检索）为分母；而 D9 之前系统只有单路 Dense，"双路"分母不存在 → **该验收在 D9 之前无法执行**。且"Milvus 不可用 → 降级 BM25"（[L584](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L584)）与"拔掉 Milvus"的降级路径在 D9 之后是两条不同路径（BM25 单路 vs 混合），语义要分开写。

**修法**：把验收拆成两条并各自绑定时点：
> - D9 前：拔掉 Milvus → 降级 **BM25 单路**，A 档成功率 ≥ 单路 Dense 的 90%（同一实现，无混合损失）；
> - D9 后：混合检索 + rerank 相比单路 Dense 的 A 档成功率不下降（≥95%），且 FR-04b 独立验收"Top-1 命中率 ≥ 单路 Dense + 5pp"。

---

#### P1-13｜北极星指标与业务价值之间没有因果链 —— 没有一条需求是"业务用户真的会用它"

- 4.1 核心问题 [L84](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L84)：痛点是"**求职者**能在 demo 里跑通一次，但说不出三件事"
- 4.4 业务场景 [L118](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L118)：业务侧痛点是"取数排队 1–2 天、口径不一、BI 答不了归因"
- 北极星 [L85](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L85)：**50 题标准题库的任务成功率**
- 5.2 需求清单 [L246-262](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L246)：14 条 FR **全部是系统能力**，没有一条是"运营每天怎么用它"

**PRD 写了两套核心问题**（求职者的"讲不清" vs 业务的"取数慢"），北极星服务前者，业务场景服务后者，**两者之间没有任何一条需求或指标把"业务价值"和"成功率"连起来**。4.3 竞品分析的落点也是"市场空白在结果可信度能否被复算"—— 这是面试叙事，不是产品论证。

结果：面试官问"**这个 Agent 到底给谁省了多少时间？**"时，PRD 里的 4.4 业务场景、4.1 北极星、9.2 指标表三张表**互不对话**，答不出来。

**修法**（成本很低，只需一段）：在 4.1 或 4.4 末尾补一段"**业务价值 → 技术指标的传导链**"：

> 业务侧现状：运营每周取数 X 次（参考场景假设值，非调研数据），单次等待 1–2 天、手工写 SQL 30 分钟；
> 本项目把"等待"从 1–2 天降到 30 秒内出数，把"口径不一致"从"每次对数"降到"定义 ID 可溯源"；
> **验证方式**：在自建数据集上以 50 题代表真实取数请求，**单题平均生成时间从人工 30 分钟 → Agent ≤10 秒**，且口径可溯源率 100%；
> 该结论的边界：**数据为合成，数字代表能力上限而非真实业务收益**，不宣称替代任何 BI 产品。

这同时给 4.2「用户调研未开展」找到了诚实的出口（用可复算的技术指标替代不可获得的用户数据）—— 与作者"不编造"的立场一致。

---

#### P1-14｜FR-01 的澄清链路是单指标串行的，C 档多指标题未定义

- 6.3.1 交互流程 [L414](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L414)：
  > 指标识别 → 检索 `metric_kb` → 返回候选集（0 / 1 / N 条）→ 唯一命中且高置信 → 直接进入 PLANNING
- 6.3.1 验收 [L453](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L453)：
  > 澄清轮次上限 **2 轮**
- 6.3.1 页面元素 [L428](file:///D:/github/Nexustask-v1.0-full.md#L428)：
  > 口径候选卡 ｜ **单选卡片组** ｜ 必须选中 1 项才可确认

4.4 的 C 档归因题 [L138](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L138)："上月退款率为什么涨了？按品类拆一下" —— **同时涉及"退款率"和"品类"两个歧义点**（退款率按单/按金额；品类按一级还是二级类目）。而 FR-01 的流程是**单指标串行**："检索 → 候选集 → 单选卡片组 → 选中 1 项"。

**多指标题会怎样？** 是先定稿退款率口径、再在第二轮澄清类目（刚好用完 2 轮）？还是一次澄清卡同时选多个（但"单选卡片组 + 必须选中 1 项"的组件设计不支持）？**PRD 未定义。** 这直接影响 C 档 14 题的成功率上限，也是面试官问"复杂问题怎么处理"的必然落点。

**修法**：把口径候选卡改为**多指标多选**（每个指标一个卡片组，可同时提交），并把澄清轮次定义从"轮次"改为"**澄清批次**"：一轮内可同时澄清所有未定稿指标；2 轮指"最多两次交互"。验收增加"≥4 条多指标题（C 档）能在**单轮**澄清内完成全部指标定稿"。

---

#### P1-15｜去掉 schema 检索工具后，"用户指定任意维度"的能力缺口未论证

- v0.1 FR-03 有 `schema_search`（检索表/字段语义，走 Milvus）
- v1.2 FR-03 工具表 [L512-520](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L512)：**7 个工具里没有 schema 检索**，改为 4 个固定粒度的 SQL 工具
- 7.1 [L1148](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1148)：LLM 只产出 `metric_key`/`definition_id`/`dimensions`/`filters`/`time_range`/`order_by`/`limit`
- 4.5 引用 [L212](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L212)：
  > 命名约定 dim_*/fact_* 前缀与 fact/dim 角色，**`schema_validator` 的规则依赖这套约定**

`schema_validator` **在本 PRD 的 7 个工具里不存在** —— 引用了一个不属于本项目的组件。

更实质的问题：**LLM 完全看不到表结构**（无 schema 检索），维度的合法集合只能来自 `metric_kb` 声明式定义里的 `dimensions` 字段。于是"用户问一个定义里没预置的维度组合"（例如"按商家结算周期拆 GMV"）**在架构上不可达**，而 4.5 的 10 张表提供了大量这种组合。**这是一次架构变更带来的能力收缩，但 PRD 没有论证这次收缩。**

**修法**（二选一）：
- **A（推荐，工作量小）**：保留"LLM 只见 `metric_kb`"的原则，但把 `metric_kb` 的 `dimensions` 字段设计成**覆盖全部 10 表的可下钻维度集**（在 4.5 明确列出每个指标允许的维度全集），并加一条验收"任意 ≤2 维组合均能生成合法 DAG，非法维度在结构校验期被拦截并回灌"；
- **B**：把 `schema_search` 加回工具注册表（8 个工具），并在 7.1 同步说明"表结构检索作为受控检索返回字段级元数据，不进入 SQL 生成路径"。

无论哪种，都要删掉 [L212] 对 `schema_validator` 的引用或把它写进工具清单。

---

### P2 级（文档卫生与一致性）

| # | 问题 | 位置 | 修法 |
|---|---|---|---|
| P2-1 | **"待确认"闭环规则与排期互锁**：3.2 [L74](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L74) 规定"「待确认」项在对应里程碑前必须闭环，**闭环前不得进入下游开发**"，而附录 B 9 项待确认的闭环时点最晚到 D28（含"面经样本清单"，闭环前 4.2 用户调研结论全是"待确认"）—— 按字面执行，**D28 之前整个项目都不能开发** | [L74](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L74) / 附录 B [L1640-1650](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1640) | 把规则改为"「待确认」项**不得成为其闭环时点之后的下游依赖**"，并把 4.2 面经样本的闭环时点从 D28 提到 D1（它是立论基础，应在开工前确认） |
| P2-2 | **D 档 12 题的拒答类型配额未定**（附录 B 第 3 项，D16 才闭环），而 9.2 已给 D 档 ≥85% 门限 | 附录 B [L1644](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1644) | 把配额提前到 D1（与口径候选文案定稿同批），并写入 9.2 作为 D 档门限的前置条件 |
| P2-3 | **归因看板统计口径与页面元素不一致**：14.3 [L1604](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1604) 说"按**题型档 × 失败类**交叉计数"，FR-11 页面元素 [L942](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L942) 说"X = 题型档**或模式**" | [L1604](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1604) / [L942](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L942) | 统一为两个下钻维度（题型档 / 模式），14.3 改为"支持题型档 × 失败类 与 模式 × 失败类 两个交叉视图" |
| P2-4 | **文件名 `PRD-nexustask-v1.0-full.md` 与内部版本 v1.2 不一致**，且 [L24](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L24) 只规定了与 v0.4 的优先级，未规定自身文件名与版本号的对应 | [L18](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L18) / [L24](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L24) | 重命名为 `PRD-nexustask-v1.2-full.md`，或在版本信息表加一行"文件名沿用首次命名，与内部版本号解耦" |
| P2-5 | **附录 A 暴露本地绝对路径与已废弃项目**：`| D:\github\SAAS-billing\PRD-saas-billing-platform-v1.0.md |`、`| analysis/... |`，而交付物是**公开仓库**（D28） | 附录 A [L1635](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1635) | 公开前把绝对路径改为仓库内相对路径（`docs/`、`analysis/`），已废弃项目只留版本号不留本地路径 |
| P2-6 | **v0.1 有、v1.2 丢掉的量化容错门限**：v0.1 NFR-05「中断恢复 ≥95%」在 v1.2 §12 非功能需求"可靠性"里只剩定性表述"进程被杀可从 checkpoint 恢复"，无数值门限 | §12 [L1489](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1489) | 补回"进程 kill -9 后恢复成功率 ≥95%（20 次注入故障实验）" |
| P2-7 | **FR-04 的压缩验收门限过松**："会话第 6 轮时，上下文 token 数不超过第 1 轮的 1.5 倍"——按 7.2.3 估算第 1 轮 ≈6k、摘要仅 0.5–1k，实际比值约 1.15，门限 1.5 测不出退化 | [L597](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L597) | 改为绝对门限"会话摘要 ≤1.5k token"或"第 6 轮 ≤ 第 1 轮 × 1.2"，并加一条"第 20 轮时摘要仍 ≤1.5k" |
| P2-8 | **FR-07 用"覆盖率 ≥70%"当验收**，是任意阈值，且没说测什么 | [L760](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L760) | 改为"三个角色的 schema 校验分支 + 结构化产物序列化/反序列化 + 契约一致性，覆盖率 ≥70% 且 **FR-07 验收第 1 条（自由文本字段为 0）必须 100% 覆盖**" |
| P2-9 | **降级链缺最有效的档位**：11.2 降级链 [L874-880](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L874) 为"关 rerank → 切备用模型 → 缩减输出 → PARTIAL"，**没有"减少工具调用/降低 LIMIT/缩小时间范围"** —— 而 token 超限时少一次 LLM 调用比关 rerank 省得多 | [L874](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L874) | 降级链插入一档"**收窄任务范围**：LIMIT 1000→100、时间粒度降级（month→quarter）、砍掉非关键维度"，并说明它优先于"切备用模型" |
| P2-10 | **FR-01 的"都不对"按钮无状态对应**：页面元素 [L430](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L430) 说"触发二次澄清或转工单"，但 20 条状态转移表里**没有"澄清中转工单"的转移**，也未定义转工单后任务终态 | [L430](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L430) / [L321-342](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L321) | 增加转移 #21：CLARIFYING → COMPLETED（终态=已转工单，`create_ticket` 幂等写入），或明确该按钮只触发二次澄清、不转工单 |
| P2-11 | **全局埋点表漏约 10 个 FR 内声明的事件**：13.1 的 21 个事件中缺 `followup_route`（FR-01 [L449](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L449)）、`memory_retrieve` / `template_reused`（FR-04）、`retrieval_compare`（FR-04b）、`role_artifact`（FR-07）、`mode_run` / `baseline_run`（FR-08）、`audit_write_failed`（FR-12）、`eval_run` / `eval_case_result` / `regression_gate`（FR-13） | 13.1 [L1499-1521](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1499) | 补入 13.1 并标注各事件的消费方（看板 / 门禁 / 调试页） |
| P2-12 | **SSE 事件表缺 `seq` 字段，但异常处理与验收都依赖它**：13 处写"前端按 `seq` 排序渲染"、"可按 seq 比对"，而 9 个事件的字段表里**没有 seq** | [L815-825](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L815) vs [L850](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L850)、[L860](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L860) | 所有事件加 `seq: int`（服务端单调递增），并补 `clarify.answered` 事件（用户提交口径后推什么，目前只有 `clarify.required`） |
| P2-13 | **降级链第 2 档"关闭 rerank"在 D9 之前无意义**，且降级链未定义"切备用模型后 schema 契约如何保证一致"（8.1 只说备用模型"必须能通过同一套 schema 契约测试"） | [L876](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L876) / [L1257](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1257) | 降级链标注"仅在 FR-04b 启用后生效"，并把备用模型的 schema 契约测试写进 8.1 的验收条目 |
| P2-14 | **FR 编号 `FR-04b` 破坏序列**（5.2 清单中插在 FR-04 与 FR-05 之间） | [L252](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L252) | 正式 PRD 用连续编号，RAG 优化并入 FR-04 或移到 P2 专项清单 |
| P2-15 | **未分配"理解预算"**：工期估算文档 §七 明确建议每天留 1–1.5h 只读当日新增代码并写 `docs/decisions/`，且"这 1.5h 不计入 139h，是额外成本"；v1.2 的 30 天排期里没有这一项，而 D28 才提到"README + 架构图 + decisions" | 14.1 [L1556-1584](file:///D:/github/NexusTask/docs/PRD-nexustask-v1.0-full.md#L1556) | 在 14.1 逐日排期加一列"当日额外 1h：读代码 + 写 3 行决策记录"，并把 `decisions/` 产出拆到每日（而不是 D28 一次性补） |

---

## 五、快速检查清单（17 项）

| # | 模块 | 检查项 | v0.1 | **v1.2** | 证据 / 缺口 |
|---|---|---|---|---|---|
| 1 | 基础信息 | tapd + 设计稿地址完整？ | ❌ | ⚠️ | 无地址；作品集项目 + 5.3"产品级前端不做"隐含无设计稿，但未显式标注"无需设计稿" |
| 2 | 基础信息 | 设计师/级别/PM/技术/测试/提出人填写？ | ❌ | ⚠️ | 项目级别已标注"不适用 S/A/B" ✓；作者/评审人/里程碑负责人为"待确认"；设计师/测试主R/需求提出人无位置 |
| 3 | 基础信息 | 改动范围明确？ | ⚠️ | ✅ | 交付形态 + 5.1 架构 + 5.2 FR 清单 + 4.5 数据模型，四维齐备 |
| 4 | 基础信息 | 联调/上线时间 + 修订记录完整？ | ❌ | ⚠️ | D5/D10/D15/D25/D30 节点 + T0 回填机制 ✓；变更记录有作者列但为"待确认"，无关注人 |
| 5 | 背景 | 四要素齐全？ | ❌ | ⚠️ | 用户/场景/问题 ✓，量化数据 ✗ |
| 6 | 背景 | 有具体量化数据？ | ❌ | ❌ | 仅"等 1–2 天"（自认行业常识性描述），无用户量级/发生率；4.2 显式声明未开展访谈 |
| 7 | 目标 | 量化目标有数值？ | ✅ | ✅ | 北极星 + 9.2 四维度 + 13.2 十项指标 + D20/D25 两轮门限 |
| 8 | 目标 | >5pd 填达成路径？ | ⚠️ | ✅ | 30 工作日逐日排期，每日可演示 + 不可砍/可让清单 + 置换规则 |
| 9 | 目标 | 评估方式明确？ | ⚠️ | ⚠️ | 门禁规则与指标计算方式明确；但 temperature=0 断言错误、5 次/3 次复跑口径不一、75%→80% 无排期 |
| 10 | 详述 | 需求列表完整？ | ⚠️ | ✅ | FR-01~14 + FR-04b，编号/简述/优先级/备注齐全 |
| 11 | 详述 | 交互逻辑 + 产品逻辑？ | ❌ | ⚠️ | 状态转移表 + 页面元素表 + SSE 事件表齐备，但 REPLANNING 目标态三处矛盾、"都不对"无状态对应、澄清卡无 answered 事件、多指标澄清未定义 |
| 12 | 详述 | MECE？ | ⚠️ | ✅ | 分层清晰、范围外明确、7.1 三种做法边界表、10.2 规则注入表 |
| 13 | 详述 | 埋点完整？ | ❌ | ⚠️ | 21 事件 + 10 指标，规范；但 13.1 漏 ~10 个 FR 内声明事件 |
| 14 | 灰度 | 标注或写方案？ | ❌ | ✅ | **明确"无需线上灰度/ABTest"** + 50 题回归替代机制 + 回滚判据 |
| 15 | 报表 | 报表需求具体？ | ❌ | ✅ | 失败归因看板：字段 + 统计口径 + 展示形式 + "无需其他报表" |
| 16 | 风险 | 资金风险判断 + 等级？ | ❌ | ⚠️ | §15 给了等级"低" + 措施；但收敛为"资金数据误读"，未按"是否跟钱相关 / 资金损失风险"框架判定 |
| 17 | 风险 | 数据泄露风险标注？ | ❌ | ⚠️ | §11.4 + §15 判断/等级/措施齐全 ✓；缺风控沟通结论与数据出境条款 |

**统计**：✅ 8 ｜ ⚠️ 9 ｜ ❌ 0（v0.1 为 ✅1 / ⚠️6 / ❌10）

---

## 六、模板税折算（作者自辩口径）

按 `analysis/2026-11-05-prd-review-rebuttal-solo-ai.md` 的口径重算：作者 R1 主张"单人项目无对应角色，正确做法是写一行『单人自研，上述角色均由本人承担』而不是造人名"。

**这条主张本轮已被部分采纳但未做完**：v1.2 在版本信息表写了"作者/评审人 = 待确认"、里程碑表写了"负责人 = 待确认"，**却仍没有那一句免责声明**。只要补这一行（0.2h），模块 1 的 6 项角色税即可闭合。

| 模块 | 标准分 | 官方分 | 折算后 | 说明 |
|---|---|---|---|---|
| 1 基础信息 | 1.0 | 0.0 | **0.6** | 补"单人自研，设计/PM/技术/测试/需求提出人均由本人承担；无需 tapd 与设计稿"→ 角色 6 项闭合（+0.5）；作者/评审人补真实姓名（+0.1） |
| 2 背景 | 1.5 | 0.2 | **0.4** | P1-13 的"业务价值 → 技术指标传导链"补上后可达 |
| 3 目标与收益 | 2.0 | 1.4 | **1.6** | P0-7 门限排期 + P0-8 算力预算 + P1-8 成本口径对齐后可达 |
| 4 详述 | 3.0 | 2.5 | **2.6** | P0-1/P0-3/P0-4/P1-14 修完可达 |
| 5 灰度 | 0.5 | 0.5 | **0.5** | 满分 |
| 6 报表 | 0.5 | 0.4 | **0.5** | 补 P2-3 口径统一后满分 |
| 7 风险合规 | 1.5 | 0.8 | **1.1** | P1-11 三条补完可达 |
| **合计** | **10.0** | **5.8** | **7.8** | **合格线以上** |

**结论：模板税约 1.0–1.2 分**（低于作者自辩的 1.55，因为 v1.2 已按模板重写）。**内容侧还需约 2.0 分才能达到 7.0**，全部集中在 P0-1 ~ P0-4、P1-13 五项。

---

## 七、按性价比排序的修补清单

| 序 | 动作 | 工时 | 解决 | 影响 |
|---|---|---|---|---|
| 1 | 13.2 任务成功率公式改为含 D 档拒答正确，或北极星分母改 38 | 0.3h | **P0-1** | 北极星定义自洽（最关键） |
| 2 | 9.1 标准答案制定改为"LLM 起草 + 人独立写 + 争议池"伪双盲 | 0.5h | **P0-2** | contested 机制真正生效 |
| 3 | checkpoint 粒度改为节点级，验收同步 | 0.5h | **P0-3** | FR-05 验收可达（容错演示点） |
| 4 | 补 G 类变更（换口径），FR-01 验收加口径切换题 | 0.5h | **P0-4** | 快路径覆盖核心场景 |
| 5 | 删除"超时模式不参与排名" | 0.1h | **P0-5** | FR-08 内部一致 |
| 6 | 区分"标准 SQL 可执行率 100%"与"contested ≤3" | 0.2h | **P0-6** | FR-13 验收可判定 |
| 7 | D26–D27 改为调优窗口，或下调最终门限至 75% | 0.2h | **P0-7** | 计划能同时满足阶段/最终门限 |
| 8 | 补评测算力预算表 | 0.5h | **P0-8** | API 成本进预算 |
| 9 | 补"业务价值 → 技术指标传导链"一段 | 1.0h | **P1-13** | 模块 2 + 面试必问 |
| 10 | 补 `dim_date` 或连续时间轴方案；修 `fact_settlement` 粒度与行数；补退款跨表不变量校验 | 1.5h | **P1-1/2/3** | 数据模型自洽，直接影响成功率 |
| 11 | 统一 REPLANNING 目标态；temperature=0 表述改写；幻觉率拆两层；L4 保留 depends_on | 1.0h | **P1-4/5/6/7** | 消除四处条款打架 |
| 12 | 成本口径双费率 + 分模式门限；延迟门限按题型分档 | 0.8h | **P1-8/9** | 指标口径一致 |
| 13 | 架构图补 create_ticket、D2 排期补两工具；澄清支持多指标；schema 检索取舍论证；补合规三条 | 2.0h | **P1-10~12/14/15** | 完整性与合规 |
| 14 | P2 全 15 项 | 2.0h | **P2-1~15** | 文档卫生 |
| | **合计** | **≈11h** | | **内容分 5.8 → 约 7.5** |

**最小可行集（3 小时）**：第 1、2、3、5、6 项 —— 全部是"两处条款互相打架"型问题，改起来只需改一句话，但每一条都会被面试官抓到。**第 9 项（P1-13 传导链）** 是唯一能同时提分和提升面试表现力的一条。

---

## 八、评审结论

**5.8 / 10.0 —— 不合格**（距"待改进"差 0.2 分，按模板税折算后约 6.8–7.0，触及合格线）。

**v1.2 相对 v0.1 的提升是真实的**：上轮 6 个设计洞解决 4 个，模块 4（详述）、5（灰度）、6（报表）、7（合规）四块达到或接近满分区间。文档已经从"方案说明书"进化为"可执行需求基线"。

**但仍有 8 个 P0**，且呈现一个新的失败模式：**v0.1 的问题是"缺失"，v1.2 的问题是"打架"** —— 同一件事在两个章节有两种规定（REPLANNING 目标态、成功率分母、复跑次数、超时是否计排名、标准 SQL 100% vs contested、D20/D25/80% 三档门限、checkpoint 粒度、审阅流程的双人假设）。这类问题最难被作者自己发现（因为每一条单独看都通顺），但**面试现场只要把两个章节并排摊开就会露**——而这恰恰是面试官的提问方式。

**给作者的三句话**：
1. **你写的是两个项目**：一个"求职演示系统"（4.1 的痛点、北极星 50 题成功率），一个"经营分析产品"（4.4 的业务链路、5.3 范围外）。当前 PRD 里它们互不引用，但同一份文档同时声称两者 —— 面试官会问"到底是哪一个"，而这题现在无解（P1-13）。
2. **把"验收标准"当作唯一的真相源**：凡是写进验收清单的，每条都要能在别的章节找到唯一对应的定义；本轮 8 个 P0 里有 6 个是"验收标准与正文定义不一致"，改法都是**以验收为准，回改正文**。
3. **单人项目的最大风险不是做不完，是自己证明自己**：伪双盲（P0-2）、跨表不变量校验（P1-3）、节点级 checkpoint（P0-3）都是"没人会替你做"的检查 —— **必须有一份独立的、不是你写的清单来卡住你**，这也是你唯一能对冲"面试官问穿"的机制。

---

*本报告由 Qoder Desktop / prd-reviewer skill 生成。评分依据 skill 内置 v1.0 评分体系；所有扣分项均可回溯到 PRD 原文行号。上轮基线：`analysis/2026-11-05-prd-review-nexustask-v0.1.md`（v0.1 = 4.4）。*
