# 智能体技能模型（Agent Skill Model）

> 基于 VDA 6.3 过程乌龟图构建的 AI Agent Skill 系统化设计方法论。

---

## 一、模型概述

**智能体技能模型**是一套用于指导 AI Agent / WorkBuddy Skill 设计与评估的系统性框架。它将工业生产中的 **VDA 6.3 过程审核乌龟图（7 要素）** 映射至 AI Agent 开发领域，确保 Skill 设计的结构化、可追溯性与可审核性。

### 为什么需要这个模型？

AI Agent Skill 开发当前面临以下问题：
- **缺乏标准化设计方法**：不同开发者设计的 Skill 结构差异大，难以复用和审核
- **行为不可追溯**：Agent 的决策过程往往是黑盒，难以定位和修复问题
- **质量不可量化**：缺乏统一的评估标准，无法判断 Skill 的"好坏"

本模型通过 **7 个可审核维度** 解决上述问题，使 Skill 设计过程可管理、可验证、可改进。

---

## 二、设计原理：为什么选择 VDA 6.3？

VDA 6.3 是德国汽车工业联合会（Verband der Automobilindustrie）发布的过程审核标准，广泛应用于制造业质量管理。其核心工具 **过程乌龟图（Process Turtle Diagram）** 通过 7 个要素全面描述一个过程：

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

这 7 个要素与 AI Agent Skill 的开发需求高度契合：

| VDA 6.3 要素 | AI Agent Skill 对应维度 | 说明 |
|---------------|------------------------|------|
| **输入（With What Info?）** | 01-Input | Skill 的目标、触发条件、数据来源 |
| **角色（Who?）** | 02-Role | Human-AI 分工、权限控制、Approval Gate |
| **过程（Process）** | 03-Process | 执行步骤、错误处理、状态管理 |
| **输出（Producing What?）** | 04-Output | 交付物、文件命名、输出格式 |
| **基础设施（Using What?）** | 05-Infrastructure | 文件存储、模型接入、工具依赖 |
| **作业指导（How?）** | 06-Work Instructions | SKILL.md 模板、版本管理、验收标准 |
| **绩效指标（How well?）** | 07-Metrics | 量化基准、红黄绿阈值、改进触发 |

---

## 三、七维度详解

### 3.1 输入（Input）—— Skill 的"为什么"和"什么时候"

**目的**：明确 Skill 的触发条件和数据需求，避免模糊激活。

**关键要素**：
- **目标（Goal）**：Skill 要解决什么问题？期望的最终状态是什么？
- **触发判断（Trigger Judgment）**：什么条件下激活这个 Skill？匹配度阈值是多少？
- **数据来源（Data Sources）**：需要读取哪些文件/数据库/API？数据格式是什么？

**示例**：
```
Goal: 帮助用户自动化处理重复性工作任务
Trigger: 用户输入包含 "自动化" / "批量处理" + 匹配度 ≥ 0.7
Data Sources: SKILL.md, templates/, config/
```

---

### 3.2 角色（Role）—— Skill 的"谁来做"

**目的**：明确 Human 与 AI 的分工，识别需要人工审批的关键节点。

**关键要素**：
- **Human-AI 分工矩阵**：哪些步骤由 AI 自动完成？哪些需要 Human 确认？
- **Approval Gate**：哪些操作必须获得 Human 明确批准才能执行？（如发送邮件、删除文件）
- **权限声明**：Skill 需要访问哪些敏感数据？权限如何控制？

**示例**：
```
AI 自动完成：读取文件、生成草稿、格式化输出
Human 确认：发送邮件、删除文件、修改系统配置
Approval Gate：L2 错误（需要 Human 选择处理策略）
```

---

### 3.3 过程（Process）—— Skill 的"怎么做"

**目的**：将 Skill 的执行过程分解为可追溯的步骤，定义错误处理策略。

**关键要素**：
- **执行流程**：按序号列出的操作步骤（Step 0, 1, 2...）
- **错误分级**：L0（自动修复）/ L1（重试）/ L2（暂停等待 Human）/ L3（终止并记录）
- **内存管理**：如何读取和更新工作记忆（MEMORY.md）？

**示例**：
```
Step 0: 读取 SKILL.md 和 MEMORY.md
Step 1: 执行核心逻辑
Step 2: 生成输出
Error Handling:
  - L0: 自动修复（如补全缺失参数）
  - L1: 重试 3 次
  - L2: 暂停，展示选项供 Human 选择
  - L3: 终止，写入 Error.md
```

---

### 3.4 输出（Output）—— Skill 的"产生什么"

**目的**：明确 Skill 的交付物和规范，确保输出的一致性和可验证性。

**关键要素**：
- **交付物清单**：Skill 会产生哪些文件？（如报告、图表、日志）
- **文件命名规范**：交付物如何命名？（如 `Project-Report-20260510-V1.0.docx`）
- **输出格式**：文本/Markdown/PDF/HTML？样式要求？

**示例**：
```
Deliverables:
  - Report-YYYYMMDD-V1.0.docx (主报告)
  - Evidence.zip (证据包)
  - Summary.md (摘要)

Naming Convention: {SkillName}-{Date}-V{Version}.{ext}
```

---

### 3.5 基础设施（Infrastructure）—— Skill 的"依赖什么"

**目的**：声明 Skill 的技术依赖，确保运行环境的可复现性。

**关键要素**：
- **文件存储结构**：Skill 相关文件如何组织？（如 `skill/` 目录结构）
- **模型接入**：使用哪些 AI 模型？模型配置如何管理？
- **工具依赖**：依赖哪些 MCP 工具或外部 API？

**示例**：
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

### 3.6 作业指导（Work Instructions）—— Skill 的"如何使用"

**目的**：提供 Skill 的使用说明和版本管理规范，降低使用门槛。

**关键要素**：
- **SKILL.md 模板**：Skill 的定义文件应该包含哪些章节？
- **版本管理**：SKILL.md 如何版本化？（如 `version: 1.0.0`）
- **验收标准**：如何判断 Skill 是否"完成"？

**示例**：
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

### 3.7 绩效指标（Metrics）—— Skill 的"好不好"

**目的**：建立量化的评估标准，驱动 Skill 的持续改进。

**关键要素**：
- **量化基准**：如何衡量 Skill 的"成功"？（如触发准确率、输出合规率）
- **红黄绿阈值**：什么情况下需要改进？（如触发准确率 < 85% → 红色）
- **改进触发机制**：如何收集反馈？如何迭代优化？

**示例**：
```
KPI 1: 触发准确率 ≥ 95% (Green) / 85-95% (Yellow) / < 85% (Red)
KPI 2: 输出合规率 ≥ 90%
KPI 3: 用户满意度 ≥ 4.0/5.0

Improvement Trigger: Red KPI → 强制复盘 + 改进计划
```

---

## 四、应用方法

### 4.1 设计新 Skill

按照 7 个维度逐项填写 `SKILL.md`：

1. **输入**：明确目标、触发条件、数据来源
2. **角色**：定义 Human-AI 分工、Approval Gate
3. **过程**：分解执行步骤、定义错误处理
4. **输出**：列出交付物、定义命名规范
5. **基础设施**：声明文件结构、模型配置、工具依赖
6. **作业指导**：编写 SKILL.md、分配版本号
7. **绩效指标**：设定 KPI、定义阈值、建立改进机制

### 4.2 审核现有 Skill

使用 **Skill 开发检查清单**（见 README）逐项确认：

- [ ] 维度一（输入）：目标已声明？触发条件已定义？匹配度阈值已设定？
- [ ] 维度二（角色）：Human 与 AI 的分工清晰？Approval Gate 已识别？
- [ ] 维度三（过程）：每步可追溯？错误分级已定义？
- [ ] 维度四（输出）：交付物清单已列明？文件命名规范已定义？
- [ ] 维度五（基础设施）：存储路径正确？模型配置已声明？
- [ ] 维度六（作业指导）：SKILL.md 模板完整？版本号已分配？
- [ ] 维度七（绩效指标）：量化基准已设定？红黄绿阈值已定义？

### 4.3 持续改进

1. **收集运行数据**：记录 Skill 的触发次数、成功率、错误类型
2. **定期评估 KPI**：对比红黄绿阈值，识别改进机会
3. **迭代优化**：更新 SKILL.md，提升触发准确率、输出合规率

---

## 五、参考案例

### 案例 1：会议纪要整理 Skill

- **输入**：触发词 "会议纪要" / "整理笔记"，匹配度 ≥ 0.7
- **角色**：AI 自动提取要点，关键决策需 Human 确认
- **过程**：Step 0-5，错误分级 L0-L3
- **输出**：MeetingNotes-YYYYMMDD-V1.0.md
- **基础设施**：依赖 `templates/MeetingNotes-Template.md`，模型 GPT-4o
- **作业指导**：SKILL.md v1.0
- **绩效指标**：输出准确率 ≥ 90%

### 案例 2：微信公众号草稿上传 Skill

- **输入**：触发词 "公众号" / "草稿箱"，匹配度 ≥ 0.6
- **角色**：AI 转换 HTML，上传统稿，发送前需 Human 确认
- **过程**：Step 0-5，错误处理 L0-L2
- **输出**：微信公众号草稿箱中的图文素材
- **基础设施**：依赖微信公众号 API，AppID 写在 SKILL.md 中
- **作业指导**：SKILL.md v1.0
- **绩效指标**：上传成功率 ≥ 98%

---

## 六、总结

**智能体技能模型**通过 7 个可审核维度，将 AI Agent Skill 的设计过程系统化、结构化、可量化。它适用于：

- ✅ **Skill 开发者**：提供结构化的设计方法论
- ✅ **质量工程师**：熟悉的 VDA 6.3 框架，易于理解和应用
- ✅ **团队协作**：统一的设计规范，降低沟通成本
- ✅ **持续改进**：量化的 KPI，驱动 Skill 不断优化

---

*本模型由阿明哥基于 VDA 6.3 过程乌龟图构建，适用于 AI Agent / WorkBuddy Skill 的系统化设计与评估。*
