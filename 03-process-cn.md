# 维度三：智能体操作步骤（Process Steps）

> 回答：这个 Skill 是怎样一步步执行的？每个步骤做什么？

---

## 执行总流程

<table style="border: none; border-collapse: collapse;">
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>用户输入</strong></td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 0</strong><br>触发判断</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 1</strong><br>读取 SKILL.md</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 2</strong><br>解析用户需求</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 3</strong><br>知识库查询</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 4</strong><br>执行任务</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 5</strong><br>错误处理</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 6</strong><br>生成交付物</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #e6f3ff;"><strong>Step 7</strong><br>记录运行日志</td>
</tr>
<tr>
<td align="center" style="border: none; font-size: 20px;">↓</td>
</tr>
<tr>
<td align="center" style="border: 3px solid white; background-color: #cce5ff;"><strong>Step 8</strong><br>呈现结果 + Approval Gate</td>
</tr>
</table>

---

## Step 0 — 触发判断

参见 `01-input-cn.md` 中的触发机制。匹配度 < 0.7 时：
- 0.4 ~ 0.7：询问用户"您是否希望使用 XXX Skill 来处理这个请求？"
- < 0.4：告知用户无法处理，可推荐其他 Skill 或通用对话

---

## Step 3 — 知识库查询规范

<table style="border: none; border-collapse: collapse; width:100%;">
<tr>
<td style="border: 3px solid white; background-color: #e6f3ff; padding: 10px;">发现相关知识条目（> 1 条）</td>
</tr>
<tr>
<td style="border: 3px solid white; background-color: #e6f3ff; padding: 10px;">按引用次数从高到低排序</td>
</tr>
<tr>
<td style="border: 3px solid white; background-color: #e6f3ff; padding: 10px;">按顺序引用，优先使用引用次数最高的知识</td>
</tr>
<tr>
<td style="border: 3px solid white; background-color: #e6f3ff; padding: 10px;">[后台自动] 该知识条目引用次数 +1</td>
</tr>
</table>

- **知识库中无相关内容**：主动从外部获取（网络搜索 / 用户提供），获取后记入知识库新建条目，并标注来源和日期
- **外部获取失败**：跳过该知识，并在 Report.md 中注明"未能找到相关知识"

---

## Step 5 — 错误处理规范

### 错误分级

| 级别 | 定义 | 处理方式 |
|------|------|----------|
| **L1 — 可恢复** | 工具调用失败、重试成功 | 自动重试（最多 3 次），记录重试次数 |
| **L2 — 需降级** | 主模型不可用、文件读取失败 | 切换备用模型/路径，继续执行 |
| **L3 — 致命** | 格式错误、权限不足、边界违反 | 停止执行，写入 Error.md，告知用户 |

### 错误记录模板（Error.md）

```markdown
# 错误记录 — <时间戳>

## 错误级别
L<X>

## 错误描述
<具体发生了什么>

## 发生位置
<Step X>: <文件名/函数名>

## 错误原因（推测）
<为什么会发生>

## 已尝试的修复措施
- <措施1> → 结果：<成功/失败>
- <措施2> → 结果：<成功/失败>

## 预防建议
<如何在 Skill.md 中避免同类错误>

## 相关日志行号
<log.md 中对应的行>
```

---

## 内存管理策略

| 类型 | 存储位置 | 更新时机 | 生命周期 |
|------|----------|----------|----------|
| **工作内存** | `<workspace>/.workbuddy/memory/YYYY-MM-DD.md` | 每次会话结束 | 当天有效 |
| **长期记忆** | `<workspace>/.workbuddy/memory/MEMORY.md` | 每次发现值得持久化的知识/决策时 | 跨会话 |
| **实例运行日志** | `<实例目录>/log.md` | 每个 Step 执行后 | 直到任务完结 |

> 跨会话协作时，下一个 Skill 实例读取 `MEMORY.md` 以获取上下文。
