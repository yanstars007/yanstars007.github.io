# 🚨 报警处理规则库 (Monitoring Rules & Memory)

> 本文件由 Agent 自动维护与进化。
> ⚠️ Sir 可以直接编辑此文件，Agent 会实时生效。

## 1. 自动忽略 (Silence / Auto-Ignore)
- 规则：凌晨 02:00 - 03:00 期间，`CPU > 90%` 报警 -> **忽略**。
  - *原因*：定时备份任务 (Cron Backup)，预期行为。
- 规则：`Java OOM` 但伴随 `GC Overhead Limit Exceeded` -> **忽略**。
  - *原因*：应用自动重启机制已生效，不影响服务。

## 2. 自动处理 (Auto-Fix)
- 规则：`Nginx 502 Bad Gateway` (连续 3 次) -> **执行 `systemctl restart nginx`**。
  - *反馈记录*：Sir 在 2026-04-12 确认“重启能解决，以后直接弄”。
- 规则：`Disk Space > 85%` -> **清理 `/tmp` 和旧日志**。
  - *反馈记录*：Sir 在 2026-04-15 确认“磁盘满了先清垃圾，别烦我”。

## 3. 必须人工确认 (Must Escalate)
- 规则：`Database Replication Lag > 10s` -> **通知 Sir**。
  - *原因*：涉及数据一致性，风险过高，需人工决策。
- 规则：`Payment API Error Rate > 1%` -> **通知 Sir**。
  - *原因*：直接影响收入，需立即介入。

---

## 📝 历史决策日志 (Decision Log)
- `2026-04-19`: 初始化规则库，导入 Sir 的历史偏好。
- `2026-04-12`: Sir 决定 Nginx 502 自动重启，减少夜间打扰。
