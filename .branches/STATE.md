# Conversation Branch 状态（自动生成，勿手改；权威状态见 state.json）

- 当前 HEAD：**checklist-wording**
- 主线版本：v3
- 最近更新：2026-09-05 00:13:50

## 主线目录
- 规则文件：`main/PROMPT.md`（唯一事实来源）
- 正式产物：`main/outputs/`（当前 2 个文件）

## 分支列表
| 分支 | 来源基准 | 实验目的 | 备注结论 | PROMPT | 产物数 | 创建时间 |
|---|---|---|---|---|---|---|
| checklist-wording | main@v3 | Checklist条目话术多变，避免固定开头词… | - | 未修改 | 0 | 2026-09-05 00:13:50 |

## 操作铁律（AI 每次工作前必读）

1. 先读本文件确认 **HEAD**；一切写入只允许发生在 HEAD 对应目录，严禁写入其他分支或归档目录。
2. HEAD=main 时，正式任务严格以 `main/PROMPT.md` 为唯一事实来源；聊天历史中出现过的
   分支实验性措辞一律不构成主线规则。
3. `main/` 在任何分支 testing 期间只读；只有 promote/rollback 会改变 main，
   且旧 main 必然已完整归档到 `archive/`，任何时候都可回滚。
4. 分支试跑必须与主线使用**同源输入**；评估维度须在试跑前写入分支 `NOTES.md`，不得事后找补。
5. 分支只有两种离场方式：`discard`（归档/删除，主线零改动）或
   `promote`（成为新主线）；是否 promote 只能由用户明确决定，AI 不得自行提升。
