# 刘宇广 / Yuguang Liu

**AI 应用开发 · Agent 后端** ｜ 南华大学 2027 届本科 ｜ 找实习 / 校招机会

一句话定位：**我把"Agent 到底做对没有"当成工程问题来做**——能定义、能测量、能复现，而不是靠感觉说它没问题。

我的三个项目有一条共同主线：**数据可信 → 执行可控 → 结果可证**。前两个是实习期间做的业务系统（代码不公开，设计公开），第三个是我自己搭的验证系统（代码完全公开）。

---

## 主推项目

### RuleArena —— 业务 Agent 上线前的执行门禁

**它解决什么**：Agent 调了工具，但没人能证明业务上真成了。工具返回 ACK 不等于业务成功，Agent 说自己成功了没人能验。

**怎么做**：三层机制，缺一不可——

1. 工具契约：只能做被批准的动作，不能自由发挥
2. 运行时门禁：调用前拦、重试幂等、返回后重读权威状态，不信 ACK
3. 独立 Oracle：按业务不变量做确定性裁决，不采信 Agent 自述

**最硬的一组数字**（真实 HTTP 重放，15 张工单 × 2 模式 × 3 次重复）：

| | 裸跑 | 加门禁 |
|---|---|---|
| 重复退款工单 | 6 / 15 | 0 / 15 |
| 多退金额 | ¥1920 | ¥0 |
| 终态正确率 | 60% | 100% |
| 正常工单误拦 | — | 0 |

**我不藏的数字**：搜索层 `pass@3 = 8/14`，但 `pass^3 = 1/14`——跑三次至少成一次有 8 个，三次次次都成只剩 1 个。发布门禁据此拒绝放行。这恰好是"为什么必须有独立运行时门禁"的论据：搜索保证不了覆盖。

**可验证**：在线 Demo 无需安装即可回放每张工单的每次调用；仓库内有冻结的结果 JSON；README 记录了四个真实运行打出来的缺陷（语义误读 / 504 未走恢复路径 / 同幂等键重放 / 理由码泄露）。

→ 仓库 https://github.com/Ygrowly/RuleArena ｜ 在线 Demo https://ygrowly.github.io/RuleArena/

### building-energy-ai-system —— 建筑能耗智能运营平台

服务外包竞赛作品，完整实现（含移动端，约 700 个文件）。

- **16 个 MCP 原子工具**：能耗查询、设备实时状态、COP 能效计算、异常检测、跨楼宇 / 时段对比、报表生成、RAG 检索、UI 组件渲染、工单草稿、Web 搜索……
- **LangGraph 三 Agent 编排**：Router（意图识别）→ Data Agent（ReAct 工具调用）→ Diagnose Agent（复合意图接力诊断）
- **数据不是随机数**：自研物理规则仿真引擎（generator / physics_rules / scenario_builder）生成能耗数据集，再灌入 PostgreSQL
- **Agent 行为有回归**：`backend/app/eval` 内置评测集，覆盖意图路由、工具选择、MCP Schema、RAG 回退与元数据过滤、工单草稿

→ https://github.com/Ygrowly/building-energy-ai-system

### PayTrace —— 支付转化异常归因诊断 Agent

核心不是"LLM 读一遍数据然后下结论"，而是一条**受治理的证据链**：

- 每条根因主张必须挂到具体工具调用产出的证据记录，带 `support_status`（SUPPORTED / PARTIAL / UNKNOWN）
- 证据不足的主张由编排器**自动降级**为 UNKNOWN，其损失移入"未解释"，降级动作写进 trace，不静默发生
- 100 个黄金场景分层管理（development / regression / holdout / adversarial），Ground Truth 与 Agent 隔离，可多 seed 复现
- 两种取证模式（固定流水线 B0 / 受治理循环 B2）共用同一套报告生成与校验，对比隔离出的变量恰好是"证据是怎么收集的"

→ https://github.com/Ygrowly/PayTrace

---

## 代码不公开的两个项目：设计公开

数驭穹图（NL2SQL 数据分析）与 EnergyOps（园区能耗运营）是我在实习期间参与开发的系统，代码属于任职公司，不便公开。它们的**设计取舍、非目标清单、开放问题**完整写在我的个人站上，每个案例都写了"为什么这么定、代价是什么"。

- **数驭穹图 —— 数据可信**：一句自然语言问句怎么变成口径正确的 SQL；生成前后各设一道闸（Schema 召回、危险语句拦截、结果验证与证据绑定）
- **EnergyOps —— 执行可控**：Agent 能调工具，但权限校验、幂等窗口、断点回补、人工确认这些口子怎么收

→ https://ygrowly.github.io

---

## 我写技术文档的三条纪律

1. **数字必标口径**：实测 / 固定评测集 / 计算事实，三者不混用。没测过的只写"设计目标"，不写成已达成绩。
2. **缺陷优先**：RuleArena 里最值钱的部分是四个真实运行打出来的缺陷，不是那张指标表——设计是推演，缺陷是事实。
3. **不把"设计上防住了什么"说成"我遇到过什么"**：前者可以讲，后者必须真发生过才讲。

---

## 技术栈

Python · FastAPI · LangGraph · MCP · PostgreSQL · Redis · DuckDB · RAG（RAGFlow）
Vue 3 · React · TypeScript · Uni-app
Docker Compose · pytest · Playwright · GitHub Actions

## 早期探索（方向验证用，不主推）

- **agentic-ticket-orchestrator** —— 告警工单编排引擎，Java Spring Boot 3.5 + LangGraph4J 与 Python FastAPI 双引擎，拖拽式流程配置 + SSE 实时推送处置过程
- **eye-diagnose-system** —— 眼底影像辅助诊断（早期课程阶段作品，已归档）

## 联系

- 邮箱：lyg3044good@gmail.com
- 个人站：https://ygrowly.github.io
- 掘金：https://juejin.cn/user/1819006196264012
