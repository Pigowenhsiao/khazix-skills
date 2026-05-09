# STATUS_skill_runtime_cleanup.md

## 本次變更
- 2026-05-09：依 Pigo 指示「全部推上去」，將 `khazix-skills` 目前全部本機變更提交並推送。
  - 先 `fetch origin`，確認本機落後 upstream `origin/main` 1 個 commit。
  - 使用臨時 stash 保護本機變更，快轉整合 upstream 後套回本機變更，無衝突。
  - 建立 commit：`9bf3919 chore: sync local skill updates and status reports`。
  - Upstream `KKKKhazix/khazix-skills.git` 以 HTTPS push 失敗：目前登入身分 `Pigowenhsiao` 無權限。
  - SSH push 也失敗：`Permission denied (publickey)`。
  - 新增 fork remote：`pigowenhsiao = https://github.com/Pigowenhsiao/khazix-skills.git`。
  - 已將 commit 推送到 `Pigowenhsiao/khazix-skills` 的 `main`。
- 依 Pigo 指示開始清理 Skill runtime 重複項。
- 保留 `E:\python_Code\Agent` 作為最多內容的 shared canonical repo，本次未修改 Agent repo。
- 建立清理報表資料夾：`skill-cleanup-reports/`。
- 建立 archive：`C:\Users\pigow\.skills_archive\2026-05-09_cleanup\`。
- 將 `.codex` 中明確屬於備份、pre-mount 或 sync-backup 的 Skill 搬到 archive：
  - `_sync_backup_changed14_20260409_180009`
  - `01-Knowledge-System\llm-wiki_backup_20260409_173507`
  - `note-update.pre-vault-mount.20260427_205150`
  - `06-Design-Media\_backup_remotion_2026-04-03_0016`
  - `02-Workflow-Ops\agent-instructions`
- 將 `.agents` 中內容 hash 完全相同的同名副本搬到 archive：
  - `connect-chrome`
  - `pptx-posters`
- 修復 Codex runtime 缺失的常用 Skill：從本地 `x-flowchart` 複製到 `C:\Users\pigow\.codex\skills\x-flowchart`。
- 第二輪清理 `.agents` 文件類同名重複：
  - 比對 `docx`、`pdf`、`pptx`、`xlsx` 根目錄版本與 `document-skills\*` 版本。
  - 由於 `document-skills\*` 版本檔案數相同但總大小較大，保留其內容。
  - 將舊根目錄版本搬到 `C:\Users\pigow\.skills_archive\2026-05-09_cleanup\agents-document-root-replaced\`。
  - 將 `document-skills\docx/pdf/pptx/xlsx` 提升到 `.agents\skills\docx/pdf/pptx/xlsx` 根目錄路徑，保留直接觸發路徑。

## 驗證結果
- `khazix-skills` 推送驗證：
  - `diff --cached --check` 已通過；提交前清理 `skills_duplicates_after_cleanup.md` 檔尾空白行。
  - `HEAD` 與 `pigowenhsiao/main` 均為 `9bf3919`。
  - `origin/main` 仍停在 `bab1783`，原因是 upstream repo 對目前登入身分沒有 push 權限。
- 清理前：
  - `.codex\skills`：152 個 `SKILL.md`
  - `.agents\skills`：227 個 `SKILL.md`
  - `.codex` 內部重複：9 組
  - `.agents` 內部重複：6 組
- 清理後：
  - `.codex\skills`：136 個 `SKILL.md`
  - `.agents\skills`：225 個 `SKILL.md`
  - `.codex` 內部重複：0 組
  - `.agents` 內部重複：4 組
- 第二輪清理後：
  - `.codex\skills`：136 個 `SKILL.md`
  - `.agents\skills`：221 個 `SKILL.md`
  - `.codex` 內部重複：0 組
  - `.agents` 內部重複：0 組
- `.agents\skills\docx/pdf/pptx/xlsx\SKILL.md` 均可讀取，frontmatter `name:` 正常。
- `x-flowchart` 已重新安裝到 Codex runtime，並通過 quick validation。
- Agent repo `E:\python_Code\Agent` 保持乾淨：`main...origin/main`，無工作區變更。
- 已產出報表：
  - `skill-cleanup-reports/skills_inventory_before.csv`
  - `skill-cleanup-reports/skills_duplicates_before.md`
  - `skill-cleanup-reports/moved_codex_backup_items.csv`
  - `skill-cleanup-reports/moved_agents_identical_duplicate_items.csv`
  - `skill-cleanup-reports/agents_duplicate_hash_check.csv`
  - `skill-cleanup-reports/skills_inventory_after_cleanup.csv`
  - `skill-cleanup-reports/skills_duplicates_after_cleanup.md`
  - `skill-cleanup-reports/agents_document_skill_file_diffs.csv`
  - `skill-cleanup-reports/promoted_agents_document_skills.csv`
  - `skill-cleanup-reports/skills_inventory_after_agents_doc_cleanup.csv`

## 若仍失敗
- 目前未發現 `.codex` runtime 內部同名重複。
- 目前未發現 `.agents` runtime 內部同名重複。
- 所有搬移都保留在 archive，尚未永久刪除。

## 下一步
- 建議開新 Codex / agent session 確認 Skill discovery 結果。
- 若新 session 啟動正常，archive 可保留 7-14 天後再決定是否永久刪除。
