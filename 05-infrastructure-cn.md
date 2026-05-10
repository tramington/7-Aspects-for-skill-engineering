# 维度五：智能体基础设施（Resources）

> 包括：**硬件/存储资源** + **模型接入**（模型 = 基础设施之一）

---

## 一、文件存储资源

### WorkBuddy 实际路径规范

> Skill 文件统一存放在 `~/.workbuddy/skills/<skill-name>/`
> 实例运行文件（每次执行产生）存放在各工作空间内或指定目录。

### Skill 模板文件夹结构

```
~/.workbuddy/skills/<skill-name>/
│
├── SKILL.md                      # 技能主文件（必填）
├── README.md                     # 使用说明
│
├── templates/                     # 模板文件夹
│   ├── report-template.docx       # 报告模板
│   ├── form-template.xlsx         # 表单模板
│   └── prompt-template.md         # 对话提示词模板
│
├── scripts/                      # 脚本文件夹
│   ├── generate-report.js         # 生成脚本
│   ├── pdf-to-markdown.py        # 转换脚本
│   └── validate.sh               # 验证脚本
│
├── database/                    # 数据库定义文件夹
│   ├── schema.json              # 数据库结构定义
│   └── seed-data.sql            # 初始化数据
│
├── wiki/                       # 知识库文件夹
│   ├── 术语表.md
│   ├── 标准索引.md
│   └── FAQ.md
│
└── references/                 # 参考文献文件夹
    ├── ISO_9001-2015.pdf        # 质量标准原文
    ├── Industry_Standard_SPC.pdf  # 行业参考文件
    └── 行业法规/                 # 子文件夹：存放具体法规文件
        └── Quality_Mgmt_System.pdf
```

### 实例运行文件夹结构（每个任务执行时生成）

```
<工作空间>/<YYYY-MM-DD-task-序号>/
│
├── log.md                      # 完整运行日志（必填）
├── Report.md                   # 执行总结/复盘报告（必填）
├── Error.md                    # 错误记录（仅出错时生成）
│
├── Dialog.html                 # 与用户的对话记录（HTML 格式备份）
│
├── TMP/                        # 临时文件（执行完毕应清理或打包）
│   ├── page1.png               # OCR 渲染图片
│   └── ...
│
└── deliverables/               # 最终交付物
    ├── Project-Report-v1.docx
    └── ...
```

---

## 二、模型接入（Model Access）

> 模型是基础设施的核心计算资源之一。

### 接入方式

| 类型 | 说明 | 示例 |
|------|------|------|
| **大语言模型（LLM）** | API 调用 | GPT-4o、Claude、DeepSeek |
| **多模态模型** | 视觉/音频/视频处理 | GPT-4V、PaddleOCR |
| **专用模型** | OCR、RAG、代码生成 | Tesseract、embedding 模型 |

### 多模型切换策略

| 策略 | 说明 | 适用场景 |
|------|------|----------|
| **固定模型** | 始终使用同一模型 | 通用 Skill，稳定性优先 |
| **按任务自动切换** | 简单任务用轻量模型，复杂任务用强模型 | 成本优化优先 |
| **用户指定** | 用户可指定使用哪个模型 | 专业用户，灵活需求 |

> **自动切换建议**：先用小模型判断任务复杂度，再决定是否切换大模型，避免对简单任务浪费成本。

### 模型配置声明（SKILL.md 中必须包含）

```yaml
model:
  primary: gpt-4o              # 主要使用模型
  fallback: gpt-4o-mini        # 主模型失败时降级
  multimodal: true             # 是否需要多模态能力
  vision_pages: 10             # 每次最多处理多少页

temperature: 0.7               # 0=确定性输出，1=创造性输出
max_tokens: 8192              # 最大输出长度
context_window: 128000         # 模型上下文窗口大小（用于截断策略）
```

### 调用安全

- API Key 不得硬编码在 SKILL.md 中，必须通过环境变量或配置中心注入
- 调用日志需脱敏（不记录用户原始 Prompt 中的敏感信息）
- 遵守各模型的 Rate Limit 和使用政策

---

## 三、已配置的 MCP 工具（WorkBuddy 实际）

| 工具 | 用途 |
|------|------|
| QQ 邮箱 MCP | 邮件发送（alias_id: alias_f2mcu4uWHYY02IwmuWpMR3zlPA） |
| 滴滴 MCP | 交通价格查询（桥接脚本：`~/.workbuddy/mcp-servers/didi-mcp-server.js`） |
