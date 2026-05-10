# 7-Aspects for AI Agent Skill Engineering

> A systematic framework for designing and evaluating AI Agent / WorkBuddy Skills, based on the **VDA 6.3 Process Turtle Diagram (7 elements)**.
>
> 基于 VDA 6.3 过程乌龟图七要素构建的 AI Agent / Skill 开发框架。

[中文版文档](README-cn.md) | [English Docs](README-en.md)

---

## What is this? / 这是什么？

This framework decomposes any AI Agent/Skill into **7 auditable aspects**, mirroring the VDA 6.3 process audit methodology used in automotive quality management:
本框架将任何 AI Agent/Skill 分解为 **7 个可审核维度**，借鉴汽车质量管理中使用的 VDA 6.3 过程审核方法：

| Aspect / 维度 | Name / 名称 | File (CN/EN) / 文件 | Description / 说明 |
|--------|------|---------------|------|
| **00** | **Model / 模型总纲** | [`00-model-cn.md`](00-model-cn.md) / [`00-model-en.md`](00-model-en.md) | Theoretical foundation / 理论基础 |
| 1 | **Input** — Goal, Trigger, Data Sources / 输入 — 目标、触发、数据来源 | [`01-input-cn.md`](01-input-cn.md) / [`01-input-en.md`](01-input-en.md) | Goal + Trigger definition / 目标 + 触发定义 |
| 2 | **Role** — Human-AI Division, Approval Gate / 角色 — 人机分工、审批门 | [`02-role-cn.md`](02-role-cn.md) / [`02-role-en.md`](02-role-en.md) | Division matrix + Approval Gate / 分工矩阵 + 审批门 |
| 3 | **Process** — Execution Flow, Error Handling / 过程 — 执行流程、错误处理 | [`03-process-cn.md`](03-process-cn.md) / [`03-process-en.md`](03-process-en.md) | Execution steps + error handling / 执行步骤 + 错误处理 |
| 4 | **Output** — Deliverables, Naming Conventions / 输出 — 交付物、命名规范 | [`04-output-cn.md`](04-output-cn.md) / [`04-output-en.md`](04-output-en.md) | Deliverable list + naming / 交付物清单 + 命名 |
| 5 | **Infrastructure** — File Structure, Model Access / 基础设施 — 文件结构、模型接入 | [`05-infrastructure-cn.md`](05-infrastructure-cn.md) / [`05-infrastructure-en.md`](05-infrastructure-en.md) | File structure + model config / 文件结构 + 模型配置 |
| 6 | **Work Instructions** — SKILL.md Template, Versioning / 作业指导 — SKILL.md 模板、版本管理 | [`06-work-instructions-cn.md`](06-work-instructions-cn.md) / [`06-work-instructions-en.md`](06-work-instructions-en.md) | SKILL.md template / SKILL.md 模板 |
| 7 | **Metrics** — KPIs, R/Y/G Thresholds, Improvement / 性能指标 — KPI、红黄绿阈值、改进 | [`07-metrics-cn.md`](07-metrics-cn.md) / [`07-metrics-en.md`](07-metrics-en.md) | KPI + R/Y/G thresholds / KPI + 红黄绿阈值 |

---

## Seven Aspects Relationship / 七维度关系

| Aspect / 维度 | Core Question / 核心问题 | Input From / 输入来源 | Output To / 输出去向 | Key Deliverables / 关键交付物 |
|--------|---------------|------------|-----------|------------------|
| 00 Model / 模型 | Why / 为什么 | - | - | Theoretical document / 理论文档 |
| 01 Input / 输入 | Why / When / 为什么 / 何时 | - | → 02/03 | Goal + Trigger / 目标 + 触发 |
| 02 Role / 角色 | Who / 谁 | ← 01 | → 03 | Division + Gate / 分工 + 门控 |
| 03 Process / 过程 | How / 如何 | ← 01/02/05/06 | → 04 | Steps + Errors / 步骤 + 错误 |
| 04 Output / 输出 | What / 什么 | ← 03 | - | Deliverable list / 交付物清单 |
| 05 Infrastructure / 基础设施 | What depends / 依赖什么 | - | → 03/06 | File + Model / 文件 + 模型 |
| 06 Work Instructions / 作业指导 | How to use / 如何使用 | - | → 03 | SKILL.md template / 模板 |
| 07 Metrics / 指标 | How good / 好不好 | → 03/04 | - | KPI + Thresholds / KPI + 阈值 |

---

## Who is this for? / 适用对象

- AI Agent / Skill **developers** who want a structured design methodology / 想要结构化设计方法的 AI Agent/Skill **开发者**
- Quality engineers familiar with **VDA 6.3** transitioning into AI workflows / 熟悉 **VDA 6.3** 并转向 AI 工作流的质量工程师
- Teams needing **auditable, traceable** Agent behavior / 需要 **可审核、可追溯** Agent 行为的团队

---

## Skill Development Checklist / Skill 开发检查清单

When creating a new Skill, confirm each item / 新建 Skill 时，逐项确认：

- [ ] **Aspect 00 (Model)**: Theory understood? / 理论已理解？
- [ ] **Aspect 1 (Input)**: Goal declared? Trigger defined? / 目标已声明？触发已定义？
- [ ] **Aspect 2 (Role)**: Human-AI division clear? / 人机分工清晰？
- [ ] **Aspect 3 (Process)**: Each step traceable? / 每步可追溯？
- [ ] **Aspect 4 (Output)**: Deliverable list defined? / 交付物清单已定义？
- [ ] **Aspect 5 (Infrastructure)**: Storage paths correct? / 存储路径正确？
- [ ] **Aspect 6 (Work Instructions)**: SKILL.md template complete? / SKILL.md 模板完整？
- [ ] **Aspect 7 (Metrics)**: Quantitative benchmarks set? / 量化基准已设定？

---

## License / 许可证

MIT

---

*Created by 阿明哥 (A Ming Ge), based on VDA 6.3 Process Turtle Diagram. / 本框架由阿明哥基于 VDA 6.3 过程乌龟图构建。*
