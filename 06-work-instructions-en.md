# Aspect 6: AI Agent Work Instructions

> Answers: What is the Skill's "work instruction manual"? What files does it include? How is versioning managed?

---

## Work Instruction File Checklist

| File | Necessity | Description |
|------|-------------|-------------|
| `SKILL.md` | **Required** | Skill main file, defines core behavior |
| Conversation templates | Recommended | Standard prompts when user triggers Skill |
| Run scripts | As needed | Executable code (JS/Python, etc.) |
| Data structure definition | As needed | JSON Schema, database structure |
| Knowledge base | As needed | Domain knowledge, terminology table, FAQ |
| Reference materials | As needed | Standard text, regulation original text |

---

## SKILL.md Standard Structure

Every Skill must include the following fields:

```yaml
---
name: example-skill
version: 1.0.0
created: 2025-01-01
updated: 2025-06-15
status: active                    # draft | review | pilot | active | deprecated
owner: Developer Name
---

# Goal & Scope
> (Core content from Aspect 1)

# Applicable Scenarios
- ...

# Permission Matrix
> (Permission matrix from Aspect 2)

# Process Steps (Summary)
> (Key step numbers from Aspect 3)

# Model Configuration
model:
  primary: gpt-4o
  fallback: gpt-4o-mini
temperature: 0.7

# Infrastructure Dependencies
tools:
  - document_converter
  - docx_generator
mcp_servers:
  - qq-mail

# Acceptance Criteria
acceptance:
  adoption_rate: "≥ 85%"
  error_rate: "≤ 2%"
  execution_time: "≤ 5 min"
```

---

## Version Management Specifications

| Rule | Description |
|------|-------------|
| Semantic versioning | `major.minor.patch` (e.g., `1.2.0`) |
| Major version change | Structural change in goal/scope/process steps |
| Minor version change | New feature/work instruction file added |
| Patch version change | Error fixes/phrasing optimization/reference update |
| Change record | Each update recorded in `updated` field at top of SKILL.md and in changelog |

---

## Deliverable Acceptance Criteria

Each Skill should specify in SKILL.md:

| Acceptance Item | Quantitative Standard | Verification Method |
|----------------|---------------------------|----------------------|
| Functional completeness | All declared features available | Test cases executed one by one |
| Output format | Conforms to templates in `templates/` | Format validation script |
| Boundary compliance | Requests beyond scope correctly rejected | Boundary test cases |
| Traceability | log.md contains complete execution path | Manual spot check |
| Error recovery | L1/L2 errors auto-handled, L3 errors have clear prompts | Simulated error injection test |

---

## Reference File Specifications

All referenced standards/regulation files:
- Stored in `references/` folder
- Naming format: `<standard-number>_<version>.<ext>`
- Multiple versions of same standard stored separately
- Citation must include version number and source (e.g., "ISO 9001, 2015 Edition")
