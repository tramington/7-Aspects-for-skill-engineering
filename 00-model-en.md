# Agent Skill Model

> A systematic methodology for designing and evaluating AI Agent / WorkBuddy Skills, based on the VDA 6.3 Process Turtle Diagram (7 elements).

---

## 1. Model Overview

The **Agent Skill Model** is a framework for guiding the design and evaluation of AI Agent / WorkBuddy Skills. It maps the **VDA 6.3 Process Turtle Diagram (7 elements)** from industrial quality management to the AI Agent development domain, ensuring structured, traceable, and auditable Skill design.

### Why do we need this model?

AI Agent Skill development currently faces these challenges:
- **Lack of standardized design methodology**: Skills designed by different developers have inconsistent structures, making them hard to reuse and audit
- **Untraceable behavior**: Agent decision-making is often a black box, making it difficult to diagnose and fix issues
- **Unquantifiable quality**: Lack of unified evaluation criteria, unable to judge Skill "goodness"

This model addresses these issues through **7 auditable dimensions**, making Skill design manageable, verifiable, and improvable.

---

## 2. Design Principle: Why VDA 6.3?

VDA 6.3 is a process audit standard published by the German Automotive Industry Association (Verband der Automobilindustrie), widely used in manufacturing quality management. Its core tool, the **Process Turtle Diagram**, describes a process through 7 elements:

```
        Who? (Roles/Competence)
              ↓
    Using What? → [PROCESS] → Producing What?
    (Infrastructure)           (Output)
              ↑
    How? (Work Instructions)
              ↑
    How well? (Metrics)
              ↑
    With What Info? (Input)
```

These 7 elements align closely with AI Agent Skill development needs:

| VDA 6.3 Element | AI Agent Skill Dimension | Description |
|-----------------|--------------------------|-------------|
| **Input (With What Info?)** | 01-Input | Skill's goal, trigger conditions, data sources |
| **Role (Who?)** | 02-Role | Human-AI division, access control, Approval Gate |
| **Process** | 03-Process | Execution steps, error handling, state management |
| **Output (Producing What?)** | 04-Output | Deliverables, file naming, output format |
| **Infrastructure (Using What?)** | 05-Infrastructure | File storage, model access, tool dependencies |
| **Work Instructions (How?)** | 06-Work Instructions | SKILL.md template, versioning, acceptance criteria |
| **Metrics (How well?)** | 07-Metrics | Quantitative benchmarks, R/Y/G thresholds, improvement triggers |

---

## 3. Seven Dimensions Explained

### 3.1 Input — The "Why" and "When" of Skill

**Purpose**: Clarify Skill's trigger conditions and data requirements, avoiding ambiguous activation.

**Key Elements**:
- **Goal**: What problem does the Skill solve? What is the desired end state?
- **Trigger Judgment**: Under what conditions is this Skill activated? What is the matching threshold?
- **Data Sources**: Which files/databases/APIs need to be read? What is the data format?

**Example**:
```
Goal: Help user automate repetitive tasks
Trigger: User input contains "automate" / "batch process" + match score ≥ 0.7
Data Sources: SKILL.md, templates/, config/
```

---

### 3.2 Role — The "Who" of Skill

**Purpose**: Clarify Human-AI division of labor, identify critical nodes requiring human approval.

**Key Elements**:
- **Human-AI Division Matrix**: Which steps are completed automatically by AI? Which require Human confirmation?
- **Approval Gate**: Which operations must obtain explicit Human approval before execution? (e.g., sending emails, deleting files)
- **Permission Declaration**: What sensitive data does the Skill need to access? How are permissions controlled?

**Example**:
```
AI Auto: Read files, generate drafts, format output
Human Confirm: Send emails, delete files, modify system config
Approval Gate: L2 errors (require Human to choose handling strategy)
```

---

### 3.3 Process — The "How" of Skill

**Purpose**: Decompose Skill's execution process into traceable steps, define error handling strategies.

**Key Elements**:
- **Execution Flow**: Numbered operation steps (Step 0, 1, 2...)
- **Error Levels**: L0 (auto-fix) / L1 (retry) / L2 (pause for Human) / L3 (terminate and log)
- **Memory Management**: How to read and update working memory (MEMORY.md)?

**Example**:
```
Step 0: Read SKILL.md and MEMORY.md
Step 1: Execute core logic
Step 2: Generate output
Error Handling:
  - L0: Auto-fix (e.g., missing param auto-completion)
  - L1: Retry 3 times
  - L2: Pause, show options for Human to choose
  - L3: Terminate, write Error.md
```

---

### 3.4 Output — The "What" of Skill

**Purpose**: Clarify Skill's deliverables and specifications, ensuring output consistency and verifiability.

**Key Elements**:
- **Deliverable List**: What files does the Skill produce? (e.g., reports, charts, logs)
- **File Naming Convention**: How are deliverables named? (e.g., `Project-Report-20260510-V1.0.docx`)
- **Output Format**: Text / Markdown / PDF / HTML? Style requirements?

**Example**:
```
Deliverables:
  - Report-YYYYMMDD-V1.0.docx (main report)
  - Evidence.zip (evidence package)
  - Summary.md (summary)

Naming Convention: {SkillName}-{Date}-V{Version}.{ext}
```

---

### 3.5 Infrastructure — The "What Depends" of Skill

**Purpose**: Declare Skill's technical dependencies, ensuring reproducibility of the runtime environment.

**Key Elements**:
- **File Storage Structure**: How are Skill-related files organized? (e.g., `skill/` directory structure)
- **Model Access**: Which AI models are used? How is model configuration managed?
- **Tool Dependencies**: Which MCP tools or external APIs are required?

**Example**:
```
File Structure:
  skill/
    SKILL.md
    references/
    scripts/
    templates/

Model: Claude 3.5 Sonnet (model_id: claude-3-5-sonnet-20241022)
Tools: mcp__qq-mail__SendMessage, mcp__didi__taxi_create_order
```

---

### 3.6 Work Instructions — The "How to Use" of Skill

**Purpose**: Provide Skill usage instructions and version management specifications, lowering the barrier to entry.

**Key Elements**:
- **SKILL.md Template**: What sections should the Skill definition file contain?
- **Version Management**: How to version SKILL.md? (e.g., `version: 1.0.0`)
- **Acceptance Criteria**: How to judge if a Skill is "complete"?

**Example**:
```markdown
# SKILL.md Template
## Trigger
## Role Definition
## Execution Steps
## Output Format
## Error Handling
## Examples
```

---

### 3.7 Metrics — The "How Good" of Skill

**Purpose**: Establish quantitative evaluation criteria, driving continuous improvement of Skills.

**Key Elements**:
- **Quantitative Benchmarks**: How to measure Skill "success"? (e.g., trigger accuracy, output compliance rate)
- **R/Y/G Thresholds**: Under what circumstances is improvement needed? (e.g., trigger accuracy < 85% → Red)
- **Improvement Trigger Mechanism**: How to collect feedback? How to iterate and optimize?

**Example**:
```
KPI 1: Trigger accuracy ≥ 95% (Green) / 85-95% (Yellow) / < 85% (Red)
KPI 2: Output compliance rate ≥ 90%
KPI 3: User satisfaction ≥ 4.0/5.0

Improvement Trigger: Red KPI → Mandatory review + improvement plan
```

---

## 4. Application Methods

### 4.1 Designing a New Skill

Fill out `SKILL.md` according to the 7 dimensions:

1. **Input**: Clarify goal, trigger conditions, data sources
2. **Role**: Define Human-AI division, Approval Gate
3. **Process**: Decompose execution steps, define error handling
4. **Output**: List deliverables, define naming conventions
5. **Infrastructure**: Declare file structure, model config, tool dependencies
6. **Work Instructions**: Write SKILL.md, assign version number
7. **Metrics**: Set KPIs, define thresholds, establish improvement mechanism

### 4.2 Auditing an Existing Skill

Use the **Skill Development Checklist** (see README) to confirm each item:

- [ ] Aspect 1 (Input): Goal declared? Trigger conditions defined? Matching threshold set?
- [ ] Aspect 2 (Role): Human-AI division clear? Approval Gate identified?
- [ ] Aspect 3 (Process): Each step traceable? Error levels defined?
- [ ] Aspect 4 (Output): Deliverable list defined? File naming conventions specified?
- [ ] Aspect 5 (Infrastructure): Storage paths correct? Model config declared?
- [ ] Aspect 6 (Work Instructions): SKILL.md template complete? Version number assigned?
- [ ] Aspect 7 (Metrics): Quantitative benchmarks set? R/Y/G thresholds defined?

### 4.3 Continuous Improvement

1. **Collect runtime data**: Record Skill trigger count, success rate, error types
2. **Regularly evaluate KPIs**: Compare R/Y/G thresholds, identify improvement opportunities
3. **Iterate and optimize**: Update SKILL.md, improve trigger accuracy, output compliance rate

---

## 5. Reference Cases

### Case 1: Meeting Notes Organizer Skill

- **Input**: Trigger words "meeting notes" / "organize notes", match score ≥ 0.7
- **Role**: AI auto-extracts key points, critical decisions require Human confirmation
- **Process**: Step 0-5, error levels L0-L3
- **Output**: MeetingNotes-YYYYMMDD-V1.0.md
- **Infrastructure**: Depends on `templates/MeetingNotes-Template.md`, model GPT-4o
- **Work Instructions**: SKILL.md v1.0
- **Metrics**: Output accuracy ≥ 90%

### Case 2: WeChat Draft Upload Skill

- **Input**: Trigger words "公众号" / "草稿箱", match score ≥ 0.6
- **Role**: AI converts HTML, uploads draft, requires Human confirmation before sending
- **Process**: Step 0-5, error handling L0-L2
- **Output**: Graphic materials in WeChat draft box
- **Infrastructure**: Depends on WeChat MP API, AppID written in SKILL.md
- **Work Instructions**: SKILL.md v1.0
- **Metrics**: Upload success rate ≥ 98%

---

## 6. Summary

The **Agent Skill Model** systematically, structurally, and quantitatively approaches AI Agent Skill design through 7 auditable dimensions. It is suitable for:

- ✅ **Skill Developers**: Provides structured design methodology
- ✅ **Quality Engineers**: Familiar VDA 6.3 framework, easy to understand and apply
- ✅ **Team Collaboration**: Unified design specifications, reducing communication costs
- ✅ **Continuous Improvement**: Quantitative KPIs, driving continuous Skill optimization

---

*This model was created by 阿明哥 (A Ming Ge), based on VDA 6.3 Process Turtle Diagram, applicable to AI Agent / WorkBuddy Skill systematic design and evaluation.*
