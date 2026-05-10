# 7-Aspects for AI Agent Skill Engineering

> An AI Agent / Skill development framework based on the VDA 6.3 Process Turtle Diagram (7 elements).
>
> **Core Logic**: Input (Goal) → Role Constraints → Process Steps → Output → Resources (Infrastructure) → Work Instructions → Metrics.

---

## Turtle Diagram (Standard Layout)

```
                    ┌──────────────────┐      ┌──────────────────┐
                    │  02-Roles        │      │ 05-Infrastructure│
                    │ (02-role-en.md)  │      │(05-infrastructure-│
                    │ Cross-cutting    │      │    en.md)        │
                    └────────┬─────────┘      └────────┬─────────┘
                             │                         │
                             ▼                         ▼
   ┌───────────────┐   ┌──────────────────────────────────────────┐   ┌───────────────┐
   │ 01-Input      │──►│                                          │──►│ 04-Output     │
   │(01-input-en.md)│   │      03-Process Steps (Skill process)    │   │(04-output-en.md)│
   │Goal+Trigger+  │   │      (03-process-en.md)                  │   │ Deliverables  │
   │  Data Sources │   │                                          │   │ + Artifacts   │
   └───────────────┘   └──────────────┬───────────────────────────┘   └───────────────┘
                                      │
                       ┌──────────────┴───────────────┐
                       │                              │
                       ▼                              ▼
              ┌──────────────────┐          ┌──────────────────┐
              │ 06-Work          │◄────────►│ 07-Metrics       │
              │ Instructions     │          │(07-metrics-en.md)│
              │(06-work-instructions-│       │ Tracking+        │
              │      en.md)      │          │ Thresholds+      │
              │ SKILL.md Template│          │ Improvement      │
              └──────────────────┘          └──────────────────┘
```

---

## File List

| Aspect | Name | File | Description |
|--------|------|------|-------------|
| **1** | Input | `01-input-en.md` | Goal, trigger judgment, data sources |
| **2** | Role | `02-role-en.md` | Human-AI division, permission matrix, Approval Gate |
| **3** | Process | `03-process-en.md` | Execution flow, error handling, memory management |
| **4** | Output | `04-output-en.md` | Deliverable classification, naming conventions |
| **5** | Resources | `05-infrastructure-en.md` | File structure + model access |
| **6** | Work Instructions | `06-work-instructions-en.md` | SKILL.md template, versioning, acceptance criteria |
| **7** | Metrics | `07-metrics-en.md` | Quantitative benchmarks, R/Y/G thresholds, improvement triggers |

---

## Skill Development Checklist

When creating a new Skill, confirm each item:

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
