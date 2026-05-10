# Aspect 4: AI Agent Output

> Answers: What is produced after this Skill finishes executing? What are the deliverables? Where are they placed?

---

## Output Classification

### 1. Direct Deliverable
Results the user expects to get, e.g.:
- Documents (8D report, quality analysis report)
- Presentation (PPT)
- Spreadsheets (Excel, CSV)
- Code files (Python, JavaScript)
- Video, images

### 2. Process Artifacts
Intermediate files generated during Skill execution:
- `log.md` — Run log (inside each instance folder)
- `Report.md` — Execution summary/review report
- `Error.md` — Error record (generated only if error occurs)
- `TMP/` — Temporary files (should be cleaned up after execution)

### 3. Updatable Artifacts
Files that can be updated after Skill execution:
- `SKILL.md` — The Skill itself (updated when new scenarios/boundaries are discovered)
- Conversation templates (optimized based on user feedback)
- Run scripts (updated when better implementations are discovered)
- Data structure definitions (Schema evolution)
- Knowledge base entries (knowledge upgrade/new additions)

---

## File Naming Conventions

| File Type | Naming Rule | Example |
|-----------|--------------|---------|
| Instance run folder | `YYYY-MM-DD-task-<index>` | `2026-05-09-task-001` |
| Run log | `log.md` | Inside above directory |
| Execution summary | `Report.md` | Inside above directory |
| Error record | `Error.md` | Inside above directory |
| Temporary files | Place in `TMP/` subdirectory | `TMP/ocr_p1.png` |
| Final deliverable | `<project>-<artifact>.<ext>` | `8D-BBP343-Report.docx` |

---

## Output Delivery Flow

```
Skill execution complete
    │
    ▼
Generate process artifacts (log.md, Report.md, Error.md)
    │
    ▼
Write deliverables to user-specified path / default working directory
    │
    ▼
Present result summary + file paths to user
    │
    ▼
[If Approval Gate involved] → Wait for user confirmation → Execute publish/send etc.
```

---

## Output Quality Requirements

| Acceptance Item | Requirement |
|----------------|-------------|
| Completeness | All declared deliverables have been generated |
| Readability | Output format correct, character encoding is UTF-8 |
| Traceability | Process artifacts (log.md) record complete execution path |
| Idempotency | Same input executed again should produce same output |
