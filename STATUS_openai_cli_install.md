# STATUS_openai_cli_install.md

## 本次變更
- 依 Pigo 指示安裝官方 `openai/openai-cli`。
- 未使用 `go install`，原因是本機 Go 為 `go1.24.5`，低於官方 README 要求的 `1.25+`。
- 改用官方 GitHub release binary：
  - 版本：`v1.1.2`
  - 檔案：`openai_1.1.2_windows_amd64.zip`
  - 安裝位置：`C:\Users\pigow\.local\bin\openai.exe`
- 另建立不與 Anaconda Python `openai.exe` 衝突的別名：
  - `C:\Users\pigow\.local\bin\openai-cli.exe`
- 依 Pigo 後續指示，移除 Anaconda 的 `openai.exe` CLI 入口點：
  - 原位置：`D:\anaconda3\Scripts\openai.exe`
  - 已搬到 archive：`C:\Users\pigow\.skills_archive\2026-05-09_cleanup\anaconda-openai-cli\openai.exe`
- 保留 Anaconda Python library `openai==2.15.0`，因為它被 `chandra-ocr` 與 `litellm` 依賴。

## 驗證結果
- 下載檔 SHA256 已比對 release digest：
  - `1407e55170e18de53577d512e46824b60e904b17df084c94f969dbc3ba2860b6`
- `C:\Users\pigow\.local\bin\openai.exe --version` 回傳：
  - `openai version 1.1.2`
- 移除 Anaconda CLI 入口點後，`openai --version` 回傳：
  - `openai version 1.1.2`
- `openai-cli --version` 回傳：
  - `openai version 1.1.2`
- `C:\Users\pigow\.local\bin\openai.exe responses --help` 可正常顯示 Responses API 指令。
- `D:\anaconda3\python.exe -c "import openai; print(openai.__version__)"` 回傳：
  - `2.15.0`

## 若仍失敗
- 目前 `openai` 已命中官方 Go CLI。
- 若未來 conda/pip 更新 `openai` 套件，可能重新產生 `D:\anaconda3\Scripts\openai.exe`，屆時需再次處理 PATH 或入口點。

## 下一步
- 如需永久避免衝突，可在 shell/profile 裡建立 `openai` alias 指向 `C:\Users\pigow\.local\bin\openai.exe`。
- 未設定 `OPENAI_API_KEY` 或 `OPENAI_ADMIN_KEY`，避免改動憑證環境。
