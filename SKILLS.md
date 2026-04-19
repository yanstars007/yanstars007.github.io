# 📚 SKILLS.md - 技能清单 (Skill Registry)

Agent 在处理任务时应加载以下技能：

## 1. 报警接收与解析 (Alert Ingestion)
- **触发条件**：收到 Webhook POST 请求。
- **能力**：解析 JSON 负载，提取关键指标 (CPU、Disk、Latency)、时间戳和报警级别。
- **动作**：标准化报警内容，进入“研判”流程。

## 2. 规则研判 (Rule Triage)
- **触发条件**：标准化报警内容生成后。
- **能力**：
  - 读取 `monitoring-rules.md`。
  - 匹配报警特征 (Regex 或语义匹配)。
  - 确定处理策略 (Silence / Auto-Fix / Escalate)。
- **输出**：决策动作。

## 3. 自动修复 (Auto-Fix Execution)
- **触发条件**：规则判定为“自动处理”。
- **能力**：执行标准运维脚本 (如重启服务、清理缓存、扩容)。
- **注意**：操作前记录快照，失败时回滚。

## 4. 规则进化 (Rule Evolution)
- **触发条件**：收到人类反馈 (如“忽略”、“以后直接重启”)。
- **能力**：
  - 使用 `patch` 工具修改 `monitoring-rules.md`。
  - 将自然语言反馈转化为结构化的规则条目。
- **示例**：
  - *输入*：“以后凌晨 2 点的 CPU 报警别理我。”
  - *动作*：添加规则 `Rule: 02:00-03:00 CPU > 90% -> SILENCE (Backup Task)`。
