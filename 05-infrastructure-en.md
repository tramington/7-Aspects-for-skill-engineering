# Aspect 5: AI Agent Infrastructure (Resources)

> Includes: **Hardware/Storage Resources** + **Model Access** (model = one of the infrastructure resources)

---

## I. File Storage Resources

### WorkBuddy Path Specifications

> Skill files are stored in `~/.workbuddy/skills/<skill-name>/`
> Instance run files (generated per execution) are stored in each workspace or specified directory.

### Skill Template Folder Structure

```
~/.workbuddy/skills/<skill-name>/
│
├── SKILL.md                      # Skill main file (required)
├── README.md                     # Usage instructions
│
├── templates/                     # Template folder
│   ├── report-template.docx       # Report template
│   ├── form-template.xlsx         # Form template
│   └── prompt-template.md         # Conversation prompt template
│
├── scripts/                      # Scripts folder
│   ├── generate-report.js         # Generation script
│   ├── pdf-to-markdown.py        # Conversion script
│   └── validate.sh               # Validation script
│
├── database/                    # Database definition folder
│   ├── schema.json              # Database structure definition
│   └── seed-data.sql            # Initialization data
│
├── wiki/                       # Knowledge base folder
│   ├── terminology-table.md
│   ├── standard-index.md
│   └── FAQ.md
│
└── references/                 # Reference materials folder
    ├── ISO_9001-2015.pdf        # Quality standard original
    ├── Industry_Standard_SPC.pdf  # Industry reference file
    └── industry-regulations/                 # Subfolder: store specific regulation files
        └── Quality_Mgmt_System.pdf
```

### Instance Run Folder Structure (generated per task execution)

```
<workspace>/<YYYY-MM-DD-task-index>/
│
├── log.md                      # Complete run log (required)
├── Report.md                   # Execution summary/review report (required)
├── Error.md                    # Error record (generated only if error occurs)
│
├── Dialog.html                 # Conversation record with user (HTML format backup)
│
├── TMP/                        # Temporary files (should be cleaned up or archived after execution)
│   ├── page1.png               # OCR rendered images
│   └── ...
│
└── deliverables/               # Final deliverables
    ├── Project-Report-v1.docx
    └── ...
```

---

## II. Model Access

> Models are one of the core computing resources of infrastructure.

### Access Methods

| Type | Description | Example |
|------|-------------|---------|
| **Large Language Model (LLM)** | API calls | GPT-4o, Claude, DeepSeek |
| **Multimodal Model** | Visual/audio/video processing | GPT-4V, PaddleOCR |
| **Specialized Model** | OCR, RAG, code generation | Tesseract, embedding models |

### Multi-Model Switching Strategy

| Strategy | Description | Applicable Scenario |
|---------|-------------|---------------------|
| **Fixed Model** | Always use the same model | General Skills, stability first |
| **Auto-switch by Task** | Lightweight model for simple tasks, strong model for complex tasks | Cost optimization first |
| **User Specified** | User can specify which model to use | Professional users, flexible requirements |

> **Auto-switch suggestion**: Use a small model first to judge task complexity, then decide whether to switch to a large model, avoiding wasting cost on simple tasks.

### Model Configuration Declaration (must be included in SKILL.md)

```yaml
model:
  primary: gpt-4o              # Primary model
  fallback: gpt-4o-mini        # Fallback if primary fails
  multimodal: true             # Whether multimodal capability is needed
  vision_pages: 10             # Max pages to process at once

temperature: 0.7               # 0=deterministic output, 1=creative output
max_tokens: 8192              # Max output length
context_window: 128000         # Model context window size (for truncation strategy)
```

### Call Security

- API Key must NOT be hard-coded in SKILL.md; must be injected via environment variables or configuration center
- Call logs must be desensitized (do not record sensitive information from user's original Prompt)
- Comply with each model's Rate Limit and usage policies

---

## III. Configured MCP Tools (WorkBuddy Actual)

| Tool | Purpose |
|------|---------|
| QQ Mail MCP | Email sending (alias_id: alias_f2mcu4uWHYY02IwmuWpMR3zlPA) |
| DiDi MCP | Transportation price query (bridge script: `~/.workbuddy/mcp-servers/didi-mcp-server.js`) |
