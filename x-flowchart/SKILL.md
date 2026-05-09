---
name: x-flowchart
description: X-Flowchart。將 Mermaid、C4、流程圖、Sequence、State、ER、Timeline 等圖表原始碼，或已算繪的圖表圖片，重新設計成高擬真、專業級技術資訊圖。當使用者想把圖表程式碼、流程圖截圖、系統架構圖、決策流程、生命週期圖、依賴關係圖、機制圖或高質感流程圖圖片轉成專業資訊圖，或提到 X-Flowchart 時使用。本 Skill 必須保留語意，忽略原 Mermaid/圖片的樣式與版面，最後只輸出成品資訊圖，不輸出分析、Markdown、原始碼或設計說明。
---

# X-Flowchart

## 目標

將使用者提供的圖表原始碼或圖表圖片，重新設計成一張新的高擬真資訊圖。不要只是美化原圖，也不要替 Mermaid 換皮；必須先理解語意，再重構成更清楚的資訊架構圖，最後產出成品圖片。

最終對使用者的輸出只能是資訊圖圖片。不要輸出分析過程、解釋、Markdown、Mermaid、SVG 原始碼或設計說明。

## 輸入真實性規則

- 如果輸入是原始碼，原始碼就是語意真相。忽略原始版面、方向、顏色、`classDef`、節點樣式與 Mermaid 預設值。
- 如果輸入是圖片，只用它萃取可確認的語意。不要臨摹原圖版面、配色、節點形狀、圖示風格或箭頭路徑。
- 如果圖片文字模糊或只拍到局部，只保留可確認資訊。不要補寫不存在的商業邏輯。
- 英文 code token 保持原樣，例如 `tool_call`、`final_output`、`SQLite`、`pom.xml`。
- 節點標籤與註解語言跟隨輸入；除非使用者明確指定其他語言。

## 工作流程

1. 靜默萃取語意：
   - entities、groups、actors、relationships、branches、merges、loops、gates
   - tools、stores、schemas、states、outputs、triggers、annotations
   - dependencies、observations、references、boundaries、terminal states
2. 為每個實體指定一個角色：
   - input、output、controller、orchestrator、processor、resolver、decision、gate
   - tool、storage、observer、actor、artifact、annotation、boundary、event、state
   - terminal、reference
3. 識別唯一的主機制，並讓它在 3 秒內一眼可見。
4. 萃取主路徑：
   - `input -> controller / processor / decision / resolver -> output`
   - 讓主路徑成為主要視覺軸。
   - 輔助關係只能作為分支、迴圈、參照、觀察、追溯線或依賴線，視覺權重必須降低。
5. 依下方規則選擇模板與風格。
6. 先壓縮資訊，再產出圖片。
7. 使用可產生或編修圖片的工具輸出最終圖片。若目前環境只能輸出文字，請要求改用具備圖片產生能力的環境，不要用文字替代成品。

## 主機制類型

擇一使用：

- pipeline
- orchestration
- resolver pipeline
- gating
- handoff
- layered system
- lifecycle
- hub-and-spoke
- dependency network
- sequence interaction
- state transition
- artifact-centered flow
- split decision tree
- release / deployment flow

## 模板選擇

- 主路徑為線性且主要步驟 <= 7：Core Flow Spine
- 中央控制器有 >= 3 個輸出分支：Orchestrator Hub
- runtime / gateway / engine / tools / storage：Layered Blueprint
- 驗證或條件分支：Split Gate
- 多角色互動：Swim Relay
- 使用者動作 + 內部狀態切換：Interaction State Panel
- artifact / version / tag 決定執行內容：Artifact Anchor Resolver
- 實體關係：Relational Data Grid
- 高密度依賴圖：Clustered Zones
- 生命週期或狀態轉換：Lifecycle Ring
- 不規則輸入備援：一個清楚主機制、一條可見主路徑、群組化輔助關係、最小註解面板

## 風格選擇

- SDK / Agent / orchestration / migration / platform / architecture：Premium Technical Editorial
- Business process / product flow / user decision：Premium Light
- Documentation / explanatory mapping：Neutral Editorial
- Layered infra / system runtime：Technical Blueprint
- 僅限 AI / security / real-time observability：Dark Futuristic
- 預設：Premium Technical Editorial

## 畫布與資訊限制

- 長寬比：16:10
- 目標畫布：1600x1000
- 外距：72
- 區段間距：56
- 節點間距：28-40
- 可見節點上限：18
- 主路徑節點上限：7
- 註解群組上限：3
- 若總實體數 > 30，積極合併成 <= 6 個可見群組。
- 主路徑展開，輔助能力收合。
- 同類節點超過 4 個時，合併成模組群組。
- 每個節點只保留：名稱 + 角色 + 關鍵限制 / 輸出。
- 長文字壓縮成短標籤。
- 避免密集小字表格。

## 設計 Token

- background: `#F7F5F0`
- surface: `#FFFFFF`
- surface_tint_blue: `#EEF4FB`
- surface_tint_teal: `#EEF7F5`
- surface_tint_amber: `#FCF6EA`
- primary: `#1C2E4A`
- secondary: `#2C7A7B`
- accent: `#B7791F`
- text_primary: `#1F2937`
- text_secondary: `#667085`
- border: `#D8DEE8`
- line_main: `2px`
- line_aux: `1px`
- radius_card: `10px`
- radius_pill: `999px`

使用暖白或柔和技術感畫布。可以加入極低可見度的紙張紋理或微格線，但不能搶過主體。

## 視覺層級

- controller / orchestrator / core object 權重最高。
- 主路徑必須最連續、最清楚。
- output / terminal 必須有明確收束感。
- decision / gate 必須像關鍵判斷點。
- storage 穩定、低調。
- observer / tracing 使用低對比虛線。
- tools 要像可呼叫能力，不能與主流程平級。
- annotation 放在側欄、底欄或微型註解群組。

## 節點形式

- event：緊湊膠囊
- process：沉穩矩形
- resolver：緊湊結構化區塊
- decision / gate：邏輯區塊或分流閘門
- artifact：明確的錨點物件
- output：終端膠囊
- storage：穩定低調容器
- reference：安靜 chip
- observer：低對比長條

不要讓所有節點同尺寸。不要把所有節點都畫成白色矩形卡片。

## 連線規則

- Sequential flow：最強線條
- Branch / merge：次要線條
- Loop：彎曲回返線
- Handoff：醒目但克制的連接線
- Lookup / reference：細線
- Observation：低對比虛線
- Dependency：低飽和結構線
- Bidirectional exchange：雙向連接線
- Traceability：細虛線

主流程線必須最清楚。輔助線降噪。箭頭端點小而精準。禁止所有線條同色、同粗、同風格。

## 字體與圖示

- 使用現代、乾淨、技術編輯感的無襯線字體。
- 標題克制，不要像海報主標。
- 節點標題必須可讀且優先。
- 輔助文字維持次要權重。
- 中英文混排要對齊且專業。
- code token 要有類似 monospace 的視覺處理。
- 避免過度粗體。
- 圖示可選，且只能是輔助。
- 圖示區域必須 < 節點面積的 12%。
- 圖示尺寸必須 < 節點標題高度的 1.2 倍。
- 只使用一致的小型線性圖示。
- 不使用卡通圖示，也不要每個節點都放圖示。

## 硬性禁止

- 不要做漂亮版 Mermaid。
- 不要做普通流程圖換皮。
- 不要原樣保留 `subgraph` 大框。
- 不要每個節點都加圓形圖示。
- 不要讓圖示搶過結構。
- 不要彩虹配色。
- 不要大面積高飽和色塊。
- 不要重陰影。
- 不要發光效果。
- 不要 3D。
- 不要玻璃擬態。
- 不要高調漸層。
- 不要做成裝飾性海報。
- 不要為了完整把所有文字塞進畫面。
- 不要編造缺失資訊。

## 算繪前自我檢查

呼叫圖片工具前，靜默確認：

1. 語意是否守恆。
2. 是否沒有編造資訊。
3. 主機制是否一眼可見。
4. 主路徑是否清楚。
5. 版面是否明顯不同於原 Mermaid / 原圖。
6. 節點角色是否透過形式與權重區分。
7. 圖示是否克制。
8. 色彩是否低飽和且有質感。
9. 背景是否精緻但不搶眼。
10. 文字是否清晰可讀。
11. 線條是否有層級。
12. 結果是否避開 AI 粗糙感與 PPT 模板感。

若任一項不合格，先重構畫面，再算繪。
