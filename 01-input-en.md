# Aspect1: AI Agent Input

> Answers: Why does this Skill start? What information does it need to read?

---

## Goal

Every Skill should declare its goal in the SKILL.md header:

```yaml
goal: >
  Help users complete a
  project report acceptable to clients,
  following standard processes.
scope:
  included:          # Applicable scope
    - Quality issue analysis
    - Project report writing
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

<table style="border: none; border-collapse: collapse;">
<tr>
<td style="border: 3px solid white; background-color: #e6f3ff; padding: 10px;"><strong>Step1: Intent Recognition</strong><br/>Model understands user semantics, judges relevance to this Skill</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td style="border: 3px solid white; background-color: #e6f3ff; padding: 10px;"><strong>Step2: Match Score Evaluation</strong><br/>Keywords + semantic similarity ≥ threshold? → Activate<br/>Low match → Deactivate</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td style="border: 3px solid white; background-color: #e6f3ff; padding: 10px;"><strong>Step3: Compliance Check</strong><br/>Within goal scope?<br/>Non-compliant → Reject with explanation</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #cce5ff; padding: 10px;"><strong>Skill Activated</strong></td>
</tr>
</table>

### Match Score Rules

| Bonus Item | Score |
|--------|------|
| Exact keyword hit ("report", "analysis", "assessment") | +0.6 |
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
| **User Request** | Initiated via direct conversation | "Help me write a project report" |
| **Workflow Input** | Upstream Skill output | JSON structured data, PDF extraction results |
| **External Data Source** | Laws/regulations, standards, knowledge base, MCP tools | ISO standard original text, ride price query |

---

## Input Quality Requirements

| Input Type | Minimum Requirement |
|----------|----------|
| Text description | Non-empty, character count ≥ 10 |
| File | Format within Skill.md declared scope, readable |
| Structured data | JSON/table format correct, contains required fields |

> If input does not meet minimum requirements, Skill should proactively ask user to supplement, rather than silently fail.
