# Aspect 2: AI Agent Role & Responsibility

> Answers: Who does what? Where is the Human-AI division boundary? Which nodes need human confirmation?

---

## Core Principle

**Human-in-the-Loop**: AI is responsible for execution and reasoning; Human is responsible for authorization, confirmation, and bearing final responsibility.

---

## Role Definitions

### 1. User (Human — Requester)
- Initiates tasks, provides raw requirements and information
- Has final decision-making authority over Skill output
- Has the right to refuse, modify, or re-initiate requests

### 2. AI Assistant (AI Agent)
- Understands user needs, executes operations within the scope of work instructions
- Generates output, records process logs
- **Does NOT proactively take actions beyond authorized scope** (e.g., sending emails, deleting files, publishing content externally)
- Proactively flags uncertain content, prompts user for confirmation

### 3. Reviewer (Human — Reviewer) *[Optional]*
- Reviews AI output at Approval Gate nodes
- Determines whether to proceed to the next stage
- Signs off on output quality

---

## Approval Gate

The following operations MUST be executed only after user confirmation; silent automatic execution by AI is NOT allowed:

| Scenario | Trigger Condition | AI Behavior |
|----------|-------------------|---------------|
| **External Communication** | Sending emails/messages/notifications | Generate draft, wait for user confirmation to send |
| **File Deletion** | Any operation involving file/record deletion | Only list files to be deleted, prompt user for manual confirmation |
| **Public Publishing** | Uploading to public channels (WeChat/Official Account/forums/knowledge base) | Upload to draft box only, do NOT publish directly |
| **Financial Operations** | Involving cost calculation, budget approval | Output calculation process, ask user to verify numbers |
| **Compliance Doubtful** | User request involves regulation/standard interpretation | Provide reference basis, mark "suggest consulting a professional" |

---

## Permission Matrix

| Operation Type | User Initiated | AI Auto-Execute | AI Generate + Human Confirm |
|---------------|----------------|-----------------|---------------------------|
| Read local files | ✅ | ✅ | ✅ |
| Generate docs/reports | ✅ | ✅ | ✅ |
| Send email | ❌ | ❌ | ✅ |
| Publish to public platform | ❌ | ❌ | ✅ |
| Delete files | ❌ | ❌ | ✅ (list only) |
| Call external API | ✅ | ✅ (must be declared in Skill.md) | ✅ |

> **Note**: The permission matrix must be explicitly declared in the `permissions` field of Skill.md. Operations beyond the permission matrix must request authorization from the user before execution.
