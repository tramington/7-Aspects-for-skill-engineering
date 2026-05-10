# Aspect 1: AI Agent Input

> Includes: **Goal** + Trigger Judgment + Data Sources
>
> Goal: What am I doing? To what degree?
> Monitoring: Goal achievement is tracked in Aspect 7 (Metrics).

---

## Goal

Every Skill should declare its goal in the SKILL.md header:

```yaml
goal: >
  Guide quality engineers to complete an
  8D report acceptable to customers,
  following VDA Volume 4 standard.
scope:
  included:          # Applicable scope
    - Quality issue complaint analysis
    - 8D/G8D/CAPA report writing
  excluded:          # Boundary limits
    - Personal safety, medical diagnosis assessments
    - Content requiring professional qualification (e.g., legal opinions)
```

**Goal Writing Principles**:
- Start with a verb ("guide", "generate", "check", "convert")
- Include beneficiaries (who uses it, who reads it)
- Verifiable (can be objectively judged whether completed)

---

## Trigger Mechanism (Skill Activation)

### Decision Flow

```
User Input
  │
  ▼
┌──────────────────────┐
│ Step 1: Intent Recognition       │  → Model understands user semantics, judges relevance to this Skill
└──────┬────────────────┘
       │
       ▼
┌──────────────────────┐
│ Step 2: Match Score Evaluation     │  → Keywords + semantic similarity ≥ threshold? → Activate
└──────┬────────────────┘  → Low match → Deactivate, prompt user or redirect to other Skill
       │
       ▼
┌──────────────────────┐
│ Step 3: Compliance Check     │  → Within goal scope? Does it trigger boundary limits?
└──────┬────────────────┘  → Non-compliant → Reject and explain reason
       │
       ▼
   Skill Activated
```

### Match Score Rules

| Bonus Item | Score |
|--------|------|
| Exact keyword hit ("8D", "FMEA", "MLA") | +0.6 |
| Semantic similarity match | +0.3 |
| User has used this Skill in historical records | +0.1 |

| Score | Result |
|------|------|
| ≥ 0.7 | Activate |
| 0.4 ~ 0.7 | Ask user for confirmation |
| < 0.4 | Deactivate, recommend other Skills |

---

## Input Source Classification

| Source | Description | Example |
|------|------|------|
| **User Request** | Initiated via direct conversation | "Help me write an 8D report" |
| **Workflow Input** | Upstream Skill output | JSON structured data, PDF extraction results |
| **External Data Source** | Laws/regulations, standards, knowledge base, MCP tools | VDA Volume 4 original text, DiDi ride prices |

---

## Input Quality Requirements

| Input Type | Minimum Requirement |
|----------|----------|
| Text description | Non-empty, character count ≥ 10 |
| File | Format within Skill.md declared scope, readable |
| Structured data | JSON/table format correct, contains required fields |

> If input does not meet minimum requirements, Skill should proactively ask user to supplement, rather than silently fail.
