# Aspect 7: AI Agent Metrics & Thresholds

> Answers: How to measure whether this Skill is doing well? When does it need improvement or refactoring?

---

## Core Metrics Definition

| Metric | Definition | Collection Method |
|--------|-------------|-------------------|
| **Model Token Usage** | Total tokens consumed per task | API logs |
| **Adoption Rate** | Proportion of users adopting/using Skill output | Manual record or feedback |
| **Runtime Error Rate** | Frequency of L3 fatal errors | Error.md statistics |
| **Knowledge Base Hit Rate** | Number of times KB entries were successfully cited | Knowledge base metadata |
| **Execution Duration** | Total time from task start to delivery | log.md timestamps |

---

## Quantitative Benchmarks & Trigger Thresholds

| Metric | Green Zone (Normal) | Yellow Zone (Warning) | Red Zone (Intervention Needed) | Trigger Action |
|---------|------------|------------|------------|---------|
| **Adoption Rate** | ≥ 85% | 60% ~ 84% | < 60% | Yellow: Optimize Skill.md → Red: Review Skill design |
| **L3 Error Rate** | < 2% | 2% ~ 5% | > 5% | Yellow: Update Error.md prevention suggestions → Red: Trigger Skill refactoring review |
| **Execution Duration** | < 5 min | 5 ~ 15 min | > 15 min | Yellow: Analyze bottleneck → Red: Consider splitting into sub-Skills |
| **KB Hit Rate** | > 70% queries have results | 40% ~ 70% | < 40% | Yellow: Supplement KB → Red: Refactor KB structure |
| **Token Consumption** | Within expectation | Expected × 1.5 | Expected × 3 | Yellow: Optimize Prompt → Red: Evaluate model selection |

---

## Knowledge Base Upgrade & Downgrade Rules

> The following are **background mechanisms**, not explicitly written into process steps, but declared in Skill.md:

```yaml
knowledge_base:
  hit_rate_threshold: 0.7    # Trigger KB review when hit rate below this value
  upgrade_rule:
    # Newly acquired external knowledge → Auto-create entry, mark source and date
  downgrade_rule:
    # Entries not cited for 30 consecutive days → Move to "archived knowledge base"
    # Archived KB entries can be deleted after 90 days
```

---

## Performance Data Recording

| Record Item | Storage Location | Update Frequency |
|-------------|-------------------|---------------------|
| Adoption rate | `~/.workbuddy/skills/<skill>/metrics.csv` | Each time user feedback is received |
| Error statistics | `~/.workbuddy/skills/<skill>/errors.csv` | Each time Error.md is generated |
| Execution duration | Same metrics.csv | Each time log.md is generated |
| KB citations | `~/.workbuddy/skills/<skill>/wiki/index.json` | Each time KB query is performed |

---

## Improvement Trigger Flow

```
Metric enters Yellow zone
  │
  ▼
Analyze root cause (view metrics.csv + Error.md)
  │
  ▼
Formulate improvement plan (update Skill.md / KB / infrastructure)
  │
  ▼
Record this improvement in Skill.md changelog
  │
  ▼
Small-scale test → Adoption rate restored to Green zone? → Officially release new version
