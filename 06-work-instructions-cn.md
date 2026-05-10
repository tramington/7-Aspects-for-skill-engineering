# 维度六：智能体作业指导（Work Instructions）

> 回答：Skill 的"作业指导书"是什么？包含哪些文件？版本如何管理？

---

## 作业指导文件清单

| 文件 | 必要性 | 说明 |
|------|--------|------|
| `SKILL.md` | **必填** | Skill 主文件，定义核心行为 |
| 对话模板 | 建议有 | 用户触发 Skill 时的标准提示词 |
| 运行脚本 | 按需 | 可执行代码（JS/Python 等） |
| 数据结构定义 | 按需 | JSON Schema、数据库结构 |
| 知识库 | 按需 | 领域知识、术语表、FAQ |
| 参考文献 | 按需 | 标准文本、法规原文 |

---

## SKILL.md 标准结构

每个 Skill 必须包含以下字段：

```yaml
---
name: vda-8d-expert
version: 1.2.0
created: 2025-06-01
updated: 2026-04-25
status: active                    # draft | review | pilot | active | deprecated
owner: 阿明哥
---

# 目标与范围
> （引用维度一的核心内容）

# 适用场景
- ...

# 权限矩阵
> （引用维度二中的权限矩阵）

# 操作步骤（概要）
> （引用维度三中的关键步骤编号）

# 模型配置
model:
  primary: gpt-4o
  fallback: gpt-4o-mini
temperature: 0.7

# 基础设施依赖
tools:
  - document_converter
  - docx_generator
mcp_servers:
  - qq-mail

# 验收标准
acceptance:
  adoption_rate: "≥ 85%"
  error_rate: "≤ 2%"
  execution_time: "≤ 5 min"
```

---

## 版本管理规范

| 规则 | 说明 |
|------|------|
| 语义化版本 | `主版本.次版本.修订号`（如 `1.2.0`） |
| 主版本变更 | 目标/范围/操作步骤发生结构性变化 |
| 次版本变更 | 新增功能/作业指导文件 |
| 修订号变更 | 修正错误/优化措辞/更新参考文献 |
| 变更记录 | 每次更新在 SKILL.md 顶部的 `updated` 和 changelog 中记录 |

---

## 交付物验收标准

每个 Skill 应在 SKILL.md 中明确：

| 验收项 | 量化标准 | 验证方式 |
|--------|----------|----------|
| 功能完整性 | 所有声明的功能点均可用 | 测试用例逐一执行 |
| 输出格式 | 符合 templates/ 中的模板格式 | 格式校验脚本 |
| 边界合规 | 超出范围的请求被正确拒绝 | 边界用例测试 |
| 可追溯性 | log.md 包含完整执行路径 | 人工抽查 |
| 错误恢复 | L1/L2 错误自动处理，L3 错误有明确提示 | 模拟错误注入测试 |

---

## 参考文件规范

所有参考的标准/法规文件：
- 存放于 `references/` 文件夹
- 命名格式：`<标准编号>_<版本>.<ext>`
- 同一标准的多个版本分开存放
- 引用时需注明版本号和来源（如"VDA Volume 4, 2nd Edition, 2020"）
