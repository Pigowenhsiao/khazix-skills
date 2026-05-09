# STATUS_aihot_skill_research.md

## 本次變更
- 研究 `aihot/SKILL.md` 的用途、觸發條件、API 路由規則、輸出格式與限制。
- 確認目前專案中沒有 `AIHOT.md`，對應 Skill 檔案是 `aihot/SKILL.md`。
- 參考 `README.md` 中 `aihot` 區塊，確認安裝方式與使用範例。

## 驗證結果
- 驗證時間：2026-05-08 20:24:44 +08:00。
- 本地搜尋：
  - `rg --files` 找到 `aihot/SKILL.md`。
  - `rg -n "AIHOT|AIHOT\.md|AI Hot|aiplus|hot" .` 找到 `aihot/SKILL.md` 與 README 相關說明。
- API 驗證：
  - `GET https://aihot.virxact.com/api/public/daily` 回傳 HTTP 200，最新日報日期為 `2026-05-08`。
  - `GET https://aihot.virxact.com/api/public/items?mode=selected&take=3` 回傳 HTTP 200，取得 3 筆精選條目。
- 注意：API 需帶瀏覽器 `User-Agent`，否則可能被 403 或連線策略擋下。

## 若仍失敗
- 無實作失敗。
- 沙盒內第一次外部連線走本機代理 `127.0.0.1` 失敗；已用允許外部連線的方式重新驗證成功。

## 下一步
- 若要實際使用此 Skill 查 AI 最新動態，預設用精選條目加時間窗。
- 只有使用者明確說「日報」時才呼叫日報端點。
- 只有使用者明確說「全部 / 完整 / 所有 / 全量」時才查全部條目。
