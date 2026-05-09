# STATUS_go_update.md

## 本次變更
- 依 Pigo 指示更新系統 Go。
- 更新前版本：
  - `go version go1.24.5 windows/amd64`
- 安裝來源：
  - `winget`
  - 套件 ID：`GoLang.Go`
- 更新後版本：
  - `go version go1.26.2 windows/amd64`

## 驗證結果
- `where.exe go` 回傳：
  - `C:\Program Files\Go\bin\go.exe`
- `go env` 關鍵值：
  - `GOROOT=C:\Program Files\Go`
  - `GOPATH=C:\Users\pigow\go`
  - `GOTOOLDIR=C:\Program Files\Go\pkg\tool\windows_amd64`
  - `GOVERSION=go1.26.2`
- `winget list --id GoLang.Go -e` 顯示：
  - `Go Programming Language amd64 go1.26.2`
- `winget upgrade --id GoLang.Go -e` 顯示：
  - 找不到可用升級，設定來源沒有更高版本。
- `openai --version` 與 `openai-cli --version` 仍正常：
  - `openai version 1.1.2`

## 若仍失敗
- `winget upgrade` 初次執行超過 5 分鐘逾時，但背景 `msiexec` 仍持續完成安裝。
- 安裝過程中 Go 曾短暫從 PATH 消失；等待 MSI 完成後恢復正常。
- 目前未發現殘留問題。

## 下一步
- 若要追最新官方 Go patch，而 winget 尚未同步，可改用官方 MSI/ZIP 手動安裝。
- 目前 Go 已高於 `openai/openai-cli` README 要求的 Go `1.25+`。
