# 7-Aspects for AI Agent Skill Engineering

> A systematic framework for designing and evaluating AI Agent / WorkBuddy Skills, based on the **VDA 6.3 Process Turtle Diagram (7 elements)**.

[中文版文档](README-cn.md) | [English Docs](README-en.md)

---

## What is this?

This framework decomposes any AI Agent/Skill into **7 auditable aspects**, mirroring the VDA 6.3 process audit methodology used in automotive quality management:

| Aspect | Name | File (CN/EN) |
|--------|------|---------------|
| 1 | **Input** — Goal, Trigger, Data Sources | [`01-input-cn.md`](01-input-cn.md) / [`01-input-en.md`](01-input-en.md) |
| 2 | **Role** — Human-AI Division, Approval Gate | [`02-role-cn.md`](02-role-cn.md) / [`02-role-en.md`](02-role-en.md) |
| 3 | **Process** — Execution Flow, Error Handling | [`03-process-cn.md`](03-process-cn.md) / [`03-process-en.md`](03-process-en.md) |
| 4 | **Output** — Deliverables, Naming Conventions | [`04-output-cn.md`](04-output-cn.md) / [`04-output-en.md`](04-output-en.md) |
| 5 | **Infrastructure** — File Structure, Model Access | [`05-infrastructure-cn.md`](05-infrastructure-cn.md) / [`05-infrastructure-en.md`](05-infrastructure-en.md) |
| 6 | **Work Instructions** — SKILL.md Template, Versioning | [`06-work-instructions-cn.md`](06-work-instructions-cn.md) / [`06-work-instructions-en.md`](06-work-instructions-en.md) |
| 7 | **Metrics** — KPIs, R/Y/G Thresholds, Improvement | [`07-metrics-cn.md`](07-metrics-cn.md) / [`07-metrics-en.md`](07-metrics-en.md) |

---

## Turtle Diagram

```
         02-Roles        05-Infrastructure
            │                   │
            ▼                   ▼
01-Input ─► 03-Process ─► 04-Output
              │
         ┌────┴────┐
         ▼         ▼
   06-Work    07-Metrics
Instructions
```

---

## Who is this for?

- AI Agent / Skill **developers** who want a structured design methodology
- Quality engineers familiar with **VDA 6.3** transitioning into AI workflows
- Teams needing **auditable, traceable** Agent behavior

---

## Skill Development Checklist

When creating a new Skill, confirm each item:

- [ ] **Aspect 1 (Input)**: Goal declared? Trigger conditions defined? Matching threshold set?
- [ ] **Aspect 2 (Role)**: Human-AI division clear? Approval Gate identified?
- [ ] **Aspect 3 (Process)**: Each step traceable? Error levels defined?
- [ ] **Aspect 4 (Output)**: Deliverable list defined? File naming conventions specified?
- [ ] **Aspect 5 (Infrastructure)**: Storage paths correct? Model config declared?
- [ ] **Aspect 6 (Work Instructions)**: SKILL.md template complete? Version number assigned?
- [ ] **Aspect 7 (Metrics)**: Quantitative benchmarks set? R/Y/G thresholds defined?

---

## License

MIT

---

*Created by 阿明哥 (A Ming Ge), based on VDA 6.3 Process Turtle Diagram.*
