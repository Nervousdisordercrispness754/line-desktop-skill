---
name: line
description: 操作 LINE 桌面版——讀取對話或傳送訊息。用法：/line read <聊天室名稱> | /line send <聊天室名稱> <訊息> | /line send! <聊天室名稱> <訊息>
argument-hint: "read <聊天室> | send <聊天室> <訊息> | send! <聊天室> <訊息>"
allowed-tools: [Bash, AskUserQuestion]
---

# LINE Skill

透過 AppleScript + cliclick 控制 macOS LINE 桌面版。不需要 LINE API token，直接操作已登入的帳號。

## 依賴工具
- `cliclick`（`brew install cliclick`）
- macOS Accessibility 權限已授予 Terminal

## 指令格式

```
/line read <聊天室名稱>           # 讀取最近對話（預設滾動 10 次）
/line read <聊天室名稱> <捲動次數> # 指定捲動深度（5=快速, 10=預設, 50=深度）
/line send <聊天室名稱> <訊息>    # 輸入訊息但不送出（手動按 Enter）
/line send! <聊天室名稱> <訊息>   # 自動送出訊息
```

## 執行流程

### 步驟 1：確認 LINE 已啟動

```bash
osascript -e 'tell application "LINE" to activate'
sleep 1
```

若 LINE 未開啟，此指令會自動啟動它。

### 步驟 2：搜尋並進入聊天室

執行以下 AppleScript（將 `CHAT_NAME` 替換為目標聊天室名稱）：

```bash
osascript << 'APPLESCRIPT'
tell application "LINE" to activate
delay 0.8
tell application "System Events"
  tell process "LINE"
    set searchField to text field 1 of splitter group 1 of window 1
    set focused of searchField to true
    delay 0.3
    key code 0 using {command down}
    key code 51
    delay 0.2
    set value of searchField to "CHAT_NAME"
    delay 0.8
    set chatList to list 1 of splitter group 1 of window 1
    click row 2 of chatList
    delay 0.5
  end tell
end tell
APPLESCRIPT
```

> row 2 是第一個搜尋結果（row 1 通常是 header）。

### 步驟 3a：讀取對話

1. 取得訊息列表位置
2. 用 cliclick 點擊中央
3. 向上捲動（每次 Page Up）
4. Cmd+A + Cmd+C 複製

```bash
# 取得訊息區座標
COORDS=$(osascript << 'APPLESCRIPT'
tell application "LINE" to activate
delay 0.3
tell application "System Events"
  tell process "LINE"
    set msgList to list 1 of splitter group 1 of splitter group 1 of window 1
    set pos to position of msgList
    set sz to size of msgList
    set cx to (round ((item 1 of pos) + (item 1 of sz) / 2))
    set cy to (round ((item 2 of pos) + (item 2 of sz) / 2))
    return (cx as text) & "," & (cy as text)
  end tell
end tell
APPLESCRIPT
)

# 點擊訊息區域
cliclick c:$COORDS
sleep 0.3

# 向上捲動 N 次（N = 捲動次數參數，預設 10）
for i in $(seq 1 10); do
  osascript -e 'tell application "System Events" to key code 116'  # Page Up
  sleep 0.05
done

# 全選並複製
osascript << 'APPLESCRIPT'
tell application "System Events"
  tell process "LINE"
    key code 0 using {command down}
    delay 0.3
    key code 8 using {command down}
    delay 0.3
  end tell
end tell
set result to the clipboard
return result
APPLESCRIPT
```

### 步驟 3b：傳送訊息

```bash
# 點擊輸入框
osascript << 'APPLESCRIPT'
tell application "LINE" to activate
delay 0.3
tell application "System Events"
  tell process "LINE"
    set inputArea to text area 1 of splitter group 1 of splitter group 1 of window 1
    click inputArea
    delay 0.3
  end tell
end tell
APPLESCRIPT

# 用剪貼板貼上訊息（支援中文）
osascript << 'APPLESCRIPT'
set the clipboard to "MESSAGE_TEXT"
tell application "System Events"
  tell process "LINE"
    key code 9 using {command down}  -- Cmd+V
    delay 0.3
  end tell
end tell
APPLESCRIPT

# 若為 send!（自動送出）
osascript -e 'tell application "System Events" to tell process "LINE" to key code 36'  # Return
```

## 注意事項

- 搜尋時會清空搜尋欄，操作完後搜尋欄會保留上次的查詢
- 對話複製上限約 50KB，超長對話會從頭截斷
- `send`（不加!）適合確認後再送，`send!` 直接送出請謹慎使用
- 圖片/貼圖在複製文字時顯示為「圖片」或「貼圖」

## 執行原則

1. 解析 `$ARGUMENTS`：第一個詞為指令（read/send/send!），第二個詞為聊天室名稱，其餘為訊息內容
2. 依序執行上述步驟
3. 讀取模式：輸出複製到的對話內容，依時間順序呈現
4. 傳送模式：確認訊息內容後執行，send! 前再次確認
