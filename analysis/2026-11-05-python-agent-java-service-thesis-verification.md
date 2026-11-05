# 调研核验：Python Agent + Java 存量系统，这条路成立吗

- 日期：2026-11-05
- 方法：WebSearch 实时检索（不用预训练知识作答），6 组查询、约 40 条结果
- 证据分级：**一手**（官方发布说明 / 基金会公告 / 规范）/ **二手**（技术媒体、框架横评）/ **⚠️ 自媒体数字**（单一来源、口径不明，仅作趋势参考）
- 性质：本文件只做**事实核验与定位修正**，产品设计见 `docs/PRD-nexustask-v0.3-dual-stack.md`

---

## 一、结论先行（三句话）

1. **你的方向对，但有一句话在 2026 年已经过时**：不能说"Java 系 Agent 不如 Python 成熟"了。Spring AI 2.0 已于 2026-06-12 GA、LangChain4j 走到 1.2x、AgentScope Java 2.0 于 2026-07 GA，三家的 MCP 客户端/服务端都是内置能力。
2. **但你的核心直觉可以换一个更硬的归因**：真正的障碍不是"Java 做不出 Agent"，而是**存量系统的运行时太旧**——Spring AI 2.0 要 Boot 4 / Framework 7 / JDK 21，而银行核心系统大量停在 Boot 2.x / JDK 8–11。在金融语境里，升级运行时**就是**"改造原系统"，而"先改造再接入，项目基本推不动"。
3. **"Python Agent 对接 Java 服务"已经不是差异化，是 2026 年的默认答案**。公开讨论里它被总结成"Python 负责推理与编排，Java 负责业务承载与事务一致性"。MCP 让工具层与语言脱钩之后，这件事的技术门槛被抹平了。**差异化必须上移**：从"能对接"上移到"**凭什么敢让它对接**"——凭据隔离、意图级授权、写操作审批、全链路审计。

一句话定位修正：

> 不是"我用 Python 写了个 Agent 去调 Java 接口"，而是"**我做了一层让 Agent 能安全操作一个它改不动的系统**"。

---

## 二、逐条核验

| # | 你的判断 | 核验结论 | 关键证据 |
|---|---|---|---|
| 1 | 传统行业（车企、国企、证券、银行）都在转型，这是巨大机会 | **成立，但"转型"不等于"上生产"** | 79% 企业已探索 Agent，仅 11% 进生产、2% 规模化（Forrester，经新浪/搜狐转载）⚠️；金融行业采用率 85%、生产部署率 58%（Adoption Report 2026）⚠️。两个口径差异大，见 §四 |
| 2 | 直接用 Java 做 Agent 可能需要在原系统上改造 | **方向成立，归因要改** | 技术归因不成立（Spring AI 可做旁路，不改被调系统）；**运行时归因成立**：Spring AI 2.0 要求 Boot 4 / Framework 7 / JDK 21，而 Boot 3.5 与 Framework 6.2 已于 2026-06-30 EOL。存量系统升级运行时＝改造 |
| 3 | Java 系 Agent 没有 Python 系成熟 | **已过时（2026 年）** | Spring AI 2.0.0 GA 2026-06-12；LangChain4j 1.2x（约 1.22，2026-10）；AgentScope Java 2.0 GA 2026-07。三家均为 Apache 2.0，均内置 MCP |
| 3b | 但新范式仍然 Python 先发 | **成立** | LangGraph（Python/TS，无 Java）、CrewAI（仅 Python）、OpenAI Agents SDK（Python/TS）、Microsoft Agent Framework（Python/.NET，Java 不在名单）。Google ADK 是唯一四语言齐发的 |
| 4 | Python Agent 对接 Java 服务是巨大优势 | **方向对，但不构成差异化** | 公开架构讨论已把"Python 编排 + Java 承载"写成 2026 默认分工；MCP 让 N×M 集成降为 N+M，工具层与语言脱钩 |
| 5 | 这套东西在互联网大厂也吃香 | **部分成立** | JD 本身是 Python 中心（"精通 Python"、"熟练 LangChain 系"），Java 双栈是加分项而非入场券；大厂更看 Agent 深度（评测、可观测、成本、并发） |

---

## 三、四条论断的展开

### 3.1 "传统行业都在转型"——成立，但要把话说准

**能说的**：金融、制造、政务是 Agent 落地的主战场，且门槛不在模型能力，在能不能接进现有体系。调研原文列举的"四道门"与你的直觉高度重合：

> 第一道是信创适配……第二道是数据不出域……第三道是审计留痕……第四道最容易被低估——老旧核心系统的对接方式：不少银行核心系统已运行十几二十年，**若要求"先改造系统再接入"，项目基本推不动；能在不改造前提下通过界面层或接口层完成对接，才是真正能落地的方案。**

**不能说的**："传统行业都在用 Agent 了"。真实分布是金字塔底部极大、顶部极小。同一批调研里另一组数字是 37% 已部署 / 33% 试点 / 20% 计划（甲子光年）——和 79/11/2 差别巨大，原因是"部署""生产""规模化"三个词在不同调研里定义不同。**面试时引用这类数字必须说明口径，否则会被一句"你这个数据哪来的"问穿。**

**对你的意义**：这条支撑"选题有价值"，但**不支撑**"我做了就能卖"。它只能当背景，不能当论据。

---

### 3.2 "Java 做 Agent 要改造原系统"——归因错了，而且上一版收得太宽

你原来的逻辑是：*Java 做 Agent → 要改原系统 → 所以不好*。这个链条在技术上不成立——Java Agent 框架可以旁路部署，通过 HTTP 调原系统的既有接口，一行不改。

上一版我给出的替代归因是"Spring AI 2.0 要 Boot 4 / JDK 21，所以要用 Java 做 Agent 就得升运行时"。**这个归因只对 Spring AI 成立，对 AgentScope 不成立**（见 §3.5）。收窄之后，准确的结论是：

```
约束不在"语言"，在"部署形态"

旁路部署（独立进程 / 独立 JVM / 独立容器）
    → 三个框架都能用，存量一行不改，只要有 JDK 17 的运行环境
    → 运行时约束基本消失

同进程集成（Agent 写进原应用，复用其 Bean / 事务 / 安全上下文）
    → 原应用的 JDK 与 Boot 版本决定你能用哪条框架线
    → JDK 8/11 的存量系统：AgentScope 与 Spring AI 2.0 都装不上（Record/Sealed Class、Boot 4 基线）
    → 这才是"改造"，而且是一个立项周期以季度计的改造
```

| 存量系统现状 | 旁路部署 | 同进程集成 |
|---|---|---|
| JDK 8 / 11（银行核心常见） | 可以（新容器自带 JDK 17） | 不行，必须升级运行时 |
| JDK 17 + Boot 3.x | 可以 | AgentScope / LangChain4j 可以；Spring AI 2.0 不行（要 Boot 4） |
| JDK 21 + Boot 4 | 可以 | 三家都可以 |

这条收窄后的结论依然有效，但**杀伤力比上一版小**：它只能说明"同进程集成在存量系统上代价高"，不能说明"Java 做不了 Agent"。**面试时如果把话说成后者，遇到懂 Java 的面试官一句话就会被拆掉。**

**注意**：新建系统、或者允许旁路部署的场景，用 Java 做 Agent 是完全合理的选择，面试时必须主动承认。

---

### 3.3 "Java 不如 Python 成熟"——这句话 2026 年说出去会被扣分

事实清单（均为 2026 年）：

| 框架 | 最新状态 | MCP | 要求 |
|---|---|---|---|
| Spring AI | 2.0.0 GA（2026-06-12），2.0.1（2026-08-21） | Client + Server 内置，`@McpTool` 注解 | Boot 4 / Framework 7 / JDK 21 |
| LangChain4j | 1.2x（2026-10 约 1.22） | Client + Server | JDK 17+，可跑 Quarkus/Micronaut/纯 Java |
| AgentScope Java | 2.0 GA（2026-07） | 支持 | JDK 17+ |

更关键的一条：**Spring AI 2.0 的 `@McpTool` 让 Java 团队一个注解就能把既有能力发布给任何 MCP 客户端**——Python Agent、Claude Code、Cursor 都能直接消费。也就是说，"Java 系统被 Python Agent 调用"在 2026 年已经是**框架内建路径**，不是需要巧思的集成方案。

那 Python 还领先在哪？领先在**新范式**：

| 框架 | Python | Java |
|---|---|---|
| LangGraph（显式图状态机 + checkpoint） | ✓ | ✗ |
| CrewAI | ✓ | ✗ |
| OpenAI Agents SDK | ✓ | ✗ |
| Microsoft Agent Framework | ✓ | ✗（仅 .NET） |
| Google ADK | ✓ | ✓ |
| Spring AI / LangChain4j | ✗ | ✓ |

所以准确的表述是：**"新范式 Python 领先一个身位，存量系统 Java 守着主场"**。这句话既诚实，又比"Java 不成熟"高级得多——它显示你知道两边各自的地盘在哪。

---

### 3.4 "Python Agent 对接 Java 服务是巨大优势"——方向对，但这是共识不是壁垒

公开讨论里已经把它总结成标准分工：

> Python 负责智能体的推理、规划与工具编排，Java 负责业务承载、事务一致性与高并发执行。

再加上协议层的变化：MCP 与 A2A 先后进入 Linux 基金会旗下的 AAIF（MCP 于 2025-12 捐赠，A2A v1.0 于 2026-03 发布），MCP SDK 月下载量级已达数亿。**"工具是什么语言写的"这件事正在变得不可见。**

结论：**做"能对接"不值钱，做"敢对接"才值钱。**

"敢对接"要回答四个问题，而协议层一个都不管：

| 问题 | 协议层（MCP/A2A） | 必须自己做的 |
|---|---|---|
| 模型能不能拿到数据库凭据？ | 不管 | 凭据持有与代调用 |
| 这个 Agent 这次能调哪些工具、能看哪些租户的数据？ | 不管 | 意图级授权、行级过滤 |
| 退款这种不可逆操作，谁能批、批了怎么防重放？ | 不管 | 审批令牌、幂等、dry-run |
| 三个月后出事，能不能说清是哪一步、哪个数据源？ | 不管 | 审计链、脱敏、trace 关联 |

这四格就是产品的全部价值。也是本节最重要的一句话。

---

### 3.5 补充核验：AgentScope Java 会不会也受运行时约束

**结论：不会。AgentScope Java 只需 JDK 17+，且不依赖 Spring Boot，可独立部署。** 这一点直接推翻"Java 做 Agent 必须升级到 JDK 21 / Boot 4"的说法。

事实（多来源一致的部分）：

| 项 | 事实 | 来源一致性 |
|---|---|---|
| 版本 | AgentScope Java 2.0 于 2026-07 GA，后续 2.0.1–2.0.3 维护版 | 高（多篇一致） |
| JDK | **17+**（用了 Record / Sealed Class / Project Reactor）；JDK 11 编译可过但运行会挂 | 高（多篇一致） |
| 框架耦合 | `agentscope-core` + `agentscope-harness` 可直接跑在普通 Maven 工程；Spring Boot Starter 是可选项 | 高 |
| 集成方式 | `@EnableAgentScope` 可让 AgentRuntime 成为 Spring 容器一等公民 | 中 |
| 编排范式 | ReAct 内核 + Pipeline / MsgHub / 子 Agent 委派；有 workspace 级状态持久化 | 中 |
| 图级能力 | **没有 LangGraph 那种"节点图 + checkpoint + `interrupt_before`"** | 中 |

> 版本细节的可信度提示：检索到的多篇自媒体对"究竟锁 JDK 17.0.8 还是 21""Spring Boot 3.1.12 才是黄金版本"给出了互相矛盾且高度具体（疑似编造）的说法。**不要引用具体小版本号**，只说"JDK 17+、框架无关、2.0 线"。

这把选型问题拆成了两个独立问题：

**问题 A：能不能用 Java 做 Agent？**
能。旁路部署一个 AgentScope Java 服务，JDK 17 容器，调既有 REST，原系统不动。**这条路上"运行时"根本不是障碍。**

**问题 B：要不要用 Java 做？**
这才是真正的选型。代价对比：

| 维度 | LangGraph (Python) | AgentScope Java 2.0 | Spring AI 2.0 |
|---|---|---|---|
| 显式状态图 + 节点 checkpoint | 原生 | 无（需自造状态机） | 无 |
| 人工审批中断（interrupt） | 原生 | 需自造 | 需自造 |
| 评测 / trace 生态（Langfuse、dataset、experiment） | 成熟 | 较弱 | 较弱 |
| RAG 组件（混合检索、rerank、Milvus） | 成熟 | 较少 | 中等 |
| 与 Java 业务系统同进程 | 不可 | 可 | 可 |
| 运行时门槛 | 有 Python | JDK 17+ | Boot 4 / JDK 21 |
| 与 JD 匹配度 | 高（JD 点名） | 低（JD 未提） | 低 |

**所以正确的说法是**：不是"Java 做不了"，而是"**这个项目的物理载体是 LangGraph 的图状态机 + checkpoint + interrupt，换成 AgentScope 得自己把这套状态机再造一遍，那就不叫用框架了**"。

**这反而是个加分项**：面试时主动说"AgentScope Java 2.0 我也评估过，JDK 17 旁路就能跑，但它是 ReAct + Pipeline 的范式，我的 10 态状态机和节点级审批中断要自己造，不如直接用 LangGraph"——比说"Java 不成熟"高一个层级。

---

## 四、证据质量与冲突（自己心里要有数）

| 结论 | 来源类型 | 可信度 | 使用建议 |
|---|---|---|---|
| Spring AI 2.0 GA 日期、依赖基线 | 多篇二手横评互相印证 + 官方发布说明转述 | 高 | 可直接引用，但面试前用官方 Release Notes 复核一次 |
| LangChain4j 版本号 | 两篇文章给出 1.20.x（2026-09）与 1.22.0（2026-10） | 中 | 说"1.2x 线"即可，别报精确小版本 |
| 79% / 11% / 2% | Forrester 调研，经新浪、搜狐转述 | 中 | 说"有调研显示"，不要说"数据显示" |
| 37% / 33% / 20% / 10% | 甲子光年白皮书，经二次解读 | 中 | 与上一行冲突，**只选一个口径用**，并说明 |
| "先改造再接入，项目基本推不动" | 行业分析文（2026-07），非官方 | 中高 | 这是定性判断不是统计，可直接引为"行业共识" |
| 41% 卡在系统集成复杂度 | CSDN 调研 N=1247，经文章转述 | 中低 ⚠️ | 仅作旁证，不作论据 |
| MCP 月下载量"数亿" | 多个二手来源说法不一（5 亿次/92.2M 周） | 低 | 不说具体数字，说"量级已是百万级项目在用" |

**通用原则**：这个领域的二手文章互相抄，同一个数字会在十篇文章里出现但只有一个源头。面试时正确姿势是——**给结论 + 说明来源类型 + 承认口径差异**，而不是背数字。

---

## 五、修正后的定位

**保留**：
- Python 做 Agent 核心（LangGraph 状态机、规划、反思、多工作流、评测）——这是 JD 的正面要求，不能动摇
- Java 做被调用的业务系统——你 3 年经验的真实资产，也是"能看懂对方接口为什么这么设计"的来源

**放弃**：
- "Java Agent 不成熟"这个论据（2026 年已被证伪）
- "Python 调 Java"作为卖点（已是共识）

**新增（真正的差异点）**：
> 一层**准入网关**：它不改被调系统一行代码，只读对方的 OpenAPI，把能力转成 Agent 可用、可授权、可审批、可审计的工具。

对应的四条设计约束，直接来自调研里企业真正卡住的地方：

| 企业门槛 | 网关的应答 |
|---|---|
| 存量系统不改造 | 只读 OpenAPI，零侵入接入；分页/错误码/单位/时间格式差异在网关侧归一化 |
| 数据不出域 | 模型只拿脱敏后的结构化摘要，原始明细不进程；网关是唯一凭据持有者 |
| 审计留痕 | 每次工具调用落审计表：谁、哪个任务、哪一步、哪个工具、参数哈希、影响行数、审批单号 |
| 权限最小化 | 意图级 scoped token：绑用户 + 任务 + 工具白名单 + 租户范围 + 15 分钟过期 |

---

## 六、给面试的三句话（可直接背）

1. **为什么不全用 Java**："Spring AI 2.0 确实能做，但我的模拟系统故意跑在 Boot 3.5 上——这就是存量系统的真实状态。要上 Spring AI 2.0 得先升到 Boot 4 + JDK 21，在金融客户那儿这一步比整个 Agent 项目还贵。"
2. **为什么不全用 Python 调库**："业务系统的账、权限、事务一致性不该被重写一遍。Agent 只负责'想'和'调'，算账还是让 Java 算。"
3. **你的差异化是什么**："不是能调通——MCP 让谁都能调通。是**调得安全**：凭据不进模型上下文、写操作要人工批、每一步可回放。"

---

## 七、引用清单

一手/准一手：
- Linux Foundation AAIF 成立与 MCP 捐赠公告（经 MIT 科技评论中文站转述）https://mittrchina.com/news/detail/15621
- Google ADK 官方 Codelab：MCP 与 A2A 配合方式 https://codelabs.developers.google.cn/getting-started-mcp-a2a-adk
- A2A 协议规范说明（Linux Foundation 托管，经 AgentCard 站转述）https://www.agentcard.net/zh

框架状态：
- Java + Python 双栈架构分界（腾讯云开发者社区，2026-10-23）https://developer.cloud.tencent.com/article/2768021
- Spring AI 2.0 GA 与 MCP 集成（51CTO，2026-09-16）https://blog.51cto.com/u_16099205/14938792
- Spring AI 2.0 架构重构解析（腾讯云，2026-08-20）https://cloud.tencent.com/developer/article/2729533
- 2026 Java 大模型框架横评：Spring AI / LangChain4j / AgentScope Java（2026-11-02）https://devpress.csdn.net/aibjcy/6ae87b10e5f4ca4eff8df2a7.html
- Python vs Java 的 Agent 框架版图与协议层作用（2026-10-12）https://blog.csdn.net/2401_85378759/article/details/167391448
- Spring AI vs LangChain4j 选型的真实分野（2026-11-01）https://blog.csdn.net/sinat_41617212/article/details/169748522

行业落地与门槛：
- 2026 金融智能体全景：四道上线门槛（2026-07-27）https://www.cnblogs.com/txgg/p/22517893
- 金融机构智能体选型：存量系统集成与信创适配 https://m.sohu.com/a/1094809167_100041230/
- 从 79% 到 2%：企业智能体落地卡在哪（新浪财经） http://cj.sina.cn/articles/view/6219345703/172b3af2700101mzsi
- 企业 Agent 采用率与漏斗（2026-10-10）https://blog.csdn.net/dx10S5j7Y/article/details/162634381
- 2026 企业 Agent 落地路径复盘：集成复杂度是首要卡点（2026-10-10）https://www.juejin.cn/post/7694628974492401715
- 2026 年 AI 技术演进与 2027 趋势前瞻（InfoQ，2026-10-30）https://www.infoq.cn/article/lmVM6XjSDMpMb6QTbK0l

协议层：
- MCP 下载量与 A2A 治理现状（2026-11-02）https://blog.csdn.net/summerliyang/article/details/169466845
- 智能体三层协同：MCP 管工具、A2A 管协作（2026-10-31）https://m.sohu.com/a/1095138500_121124777/
