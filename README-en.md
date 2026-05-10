# 7-Aspects for AI Agent Skill Engineering

> An AI Agent / Skill development framework based on the VDA 6.3 Process Turtle Diagram (7 elements).
>
> **Core Logic**: Input (Goal) → Role Constraints → Process Steps → Output → Resources (Infrastructure) → Work Instructions → Metrics.

---

## File List

| ID | Aspect | Name | File | Description |
|----|--------|------|------|-------------|
| **00** | **Model** | Agent Skill Model | `00-model-en.md` | Theoretical foundation, design principles, 7-aspect details |
| **01** | Input | Input | `01-input-en.md` | Goal, trigger judgment, data sources |
| **02** | Role | Role | `02-role-en.md` | Human-AI division, permission matrix, Approval Gate |
| **03** | Process | Process | `03-process-en.md` | Execution flow, error handling, memory management |
| **04** | Output | Output | `04-output-en.md` | Deliverable classification, naming conventions |
| **05** | Resources | Infrastructure | `05-infrastructure-en.md` | File structure + model access |
| **06** | Work Instructions | Work Instructions | `06-work-instructions-en.md` | SKILL.md template, versioning, acceptance criteria |
| **07** | Metrics | Metrics | `07-metrics-en.md` | Quantitative benchmarks, R/Y/G thresholds, improvement triggers |

---

## Seven Aspects Relationship Table

| Aspect | Core Question | Input From | Output To | Key Deliverables |
|--------|---------------|------------|-----------|------------------|
| 00 Model | Why / What | - | - | Theoretical document |
| 01 Input | Why / When trigger | - | → 02/03 | Goal + Trigger definition |
| 02 Role | Who / Who approves | ← 01 | → 03 | Division matrix + Approval Gate |
| 03 Process | How / What if error | ← 01/02/05/06 | → 04 | Execution steps + error handling |
| 04 Output | What produced / What format | ← 03 | - | Deliverable list + naming convention |
| 05 Infrastructure | What depends / Where runs | - | → 03/06 | File structure + model config |
| 06 Work Instructions | How to use / Versioning | - | → 03 | SKILL.md template |
| 07 Metrics | How good / How improve | → 03/04 | - | KPI + R/Y/G thresholds |

---

## Skill Development Checklist

When creating a new Skill, confirm each item:

- [ ] **Aspect 00**: Model theory understood? VDA 6.3 mapping clarified?
- [ ] **Aspect 1 (Input)**: Goal declared? Trigger conditions defined? Matching threshold set?
- [ ] **Aspect 2 (Role)**: Human-AI division clear? Approval Gate identified? Permission matrix declared?
- [ ] **Aspect 3 (Process)**: Each step traceable? Error levels defined? Error.md template available?
- [ ] **Aspect 4 (Output)**: Deliverable list defined? File naming conventions specified?
- [ ] **Aspect 5 (Resources)**: Storage paths correct? Model config declared? MCP tools listed?
- [ ] **Aspect 6 (Work Instructions)**: SKILL.md template complete? Version number assigned? Acceptance criteria defined?
- [ ] **Aspect 7 (Metrics)**: Quantitative benchmarks set? R/Y/G thresholds defined? Improvement trigger mechanism in place?

---

## Lifecycle States

```
Draft → Review → Pilot → Active → Deprecated
```

- **Draft**: SKILL.md written but not yet validated
- **Review**: Tested by at least 2 different users
- **Pilot**: Running in real scenarios with logs available
- **Active**: Validated through Pilot, meets acceptance criteria
- **Deprecated**: Replaced by newer version or no longer maintained

---

*This framework was created by 阿明哥 (A Ming Ge), based on VDA 6.3 Process Turtle Diagram, applicable to AI Agent / WorkBuddy Skill systematic design and evaluation.*
