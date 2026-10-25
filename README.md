<div align="center">

# 刘宇广 · Yuguang Liu

**AI 应用开发 / Agent 后端** ｜ 南华大学 2027 届 ｜ 找实习 · 校招

[![Blog](https://img.shields.io/badge/Blog-ygrowly.github.io-4C8BF5?style=for-the-badge&logo=astro&logoColor=white)](https://ygrowly.github.io)
[![Email](https://img.shields.io/badge/Email-lyg3044good%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:lyg3044good@gmail.com)
[![掘金](https://img.shields.io/badge/掘金-技术文章-1E80FF?style=for-the-badge&logo=juejin&logoColor=white)](https://juejin.cn/user/1819006196264012)

**我把「Agent 到底做对没有」当成工程问题来做** —— 能定义、能测量、能复现，而不是靠感觉说它没问题。

</div>

## 主线

**数据可信 → 执行可控 → 结果可证**。前两条是实习期间做的业务系统（代码不公开），第三条是我自己搭的验证系统（完全开源）。

| | 项目 | 一句话 | 代码 |
|---|---|---|---|
| 数据可信 | 数驭穹图 | 自然语言问句怎么变成口径正确的 SQL | 实习，未公开 · [设计](https://ygrowly.github.io) |
| 执行可控 | EnergyOps | Agent 能调工具，权限/幂等/回补怎么收口 | 实习，未公开 · [设计](https://ygrowly.github.io) |
| **结果可证** | **RuleArena** | 用数据证明 Agent 没做错，否则拒绝放行 | **开源 · 可验证** |

## 开源项目

### [RuleArena](https://github.com/Ygrowly/RuleArena) — 业务 Agent 上线前的执行门禁

[![Live Demo](https://img.shields.io/badge/在线_Demo-免安装直接打开-28A745?style=flat&logo=googlechrome&logoColor=white)](https://ygrowly.github.io/RuleArena/)

工具契约 + 运行时门禁 + 独立 Oracle：Agent 的每个动作先过检查，最后由独立账本裁决，不采信 Agent 自述。

> **同一份退款 Agent 代码跑两次**：裸跑 15 张工单里 6 张重复退款、合计多退 ¥1920 → 加门禁后 **0 笔**，正常工单误拦 0。（15 张工单 × 2 模式 × 3 次重复，真实 HTTP 重放）

### [PayTrace](https://github.com/Ygrowly/PayTrace) — 支付转化异常归因诊断 Agent

一条**受治理的证据链**：每条根因主张必须挂到具体工具调用产出的证据；证据不足的主张自动降级为 `UNKNOWN`、损失移入"未解释"，降级动作写进 trace，不静默发生。100 个黄金场景分层管理，可多 seed 复现。

### [building-energy-ai-system](https://github.com/Ygrowly/building-energy-ai-system) — 建筑能耗智能运营平台

16 个 MCP 原子工具 + LangGraph 三 Agent 编排 + RAG，含 Web 管理端与 Uni-app 移动双端；`backend/app/eval` 内置 Agent 评测集，改 prompt 能跑回归看有没有退化。服务外包竞赛作品，README 里如实写了它没做到什么。

<div align="center">

[![skillicons](https://skillicons.dev/icons?i=python,fastapi,postgresql,redis,docker,react,vue,java,spring,typescript&perline=10&theme=light)](https://skillicons.dev)

</div>

<details>
<summary><b>展开：我怎么写技术文档（3 条纪律）· 早期探索 · 开源贡献</b></summary>

<br>

**写文档的三条纪律**

1. **数字必标口径** —— 实测 / 固定评测集 / 计算事实，三者不混用；没测过的只写"设计目标"。
2. **缺陷优先** —— RuleArena 里最值钱的是四个真实运行打出来的缺陷（语义误读 / 504 未走恢复路径 / 同幂等键重放 / 理由码泄露），不是那张指标表。设计是推演，缺陷是事实。
3. **不把"设计上防住了什么"说成"我遇到过什么"**。

**我不藏的数字**：RuleArena 搜索层 `pass@3 = 8/14`，但 `pass^3 = 1/14` —— 跑三次次次都成只剩 1 个，发布门禁据此拒绝放行。这恰好是"为什么必须有独立运行时门禁"的论据：搜索保证不了覆盖。

**早期探索**（方向验证用，不主推）

- `agentic-ticket-orchestrator` —— 告警工单编排，Java Spring Boot 3.5 + LangGraph4J 与 Python FastAPI 双引擎
- `eye-diagnose-system` —— 眼底影像辅助诊断，已归档

**开源贡献**：正在向外部仓库提交真实修复（长期项，不做自家仓库的样式装修）。

</details>

---

<div align="center">

正在找 **AI 应用开发 / Agent 后端** 方向的实习与校招机会，邮箱见顶部。

</div>
