# line-desktop-skill

A [Claude Code](https://claude.ai/code) skill that controls the **LINE desktop app** on macOS via AppleScript — read chat history and send messages without any API token.

## Features

- Read recent chat history from any chat room or group
- Send messages (manual confirm or auto-send)
- No LINE API token required — operates through your already logged-in desktop app
- Supports Chinese and other CJK characters via clipboard input

## Requirements

- macOS with LINE desktop app installed and logged in
- [cliclick](https://github.com/BlueM/cliclick) — `brew install cliclick`
- Accessibility permission granted to Terminal (System Settings → Privacy & Security → Accessibility)

## Installation

Copy `skill.md` to your Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/line
cp skill.md ~/.claude/skills/line/skill.md
```

## Usage

```
/line read <chat name>              # Read recent messages (default: 10 scrolls)
/line read <chat name> <n>          # Read with custom scroll depth (5=quick, 50=deep)
/line send <chat name> <message>    # Stage message without sending (manual Enter)
/line send! <chat name> <message>   # Send message automatically
```

### Examples

```
/line read 家人
/line read 工作群組 30
/line send 小明 明天幾點？
/line send! 家人 晚餐在哪
```

## How It Works

1. Activates the LINE desktop app (launches it if not running)
2. Uses AppleScript Accessibility API to search and navigate to the target chat
3. For reading: uses `cliclick` to focus the message area, scrolls up with Page Up, then selects all and copies via clipboard
4. For sending: pastes message text via clipboard (CJK-safe), optionally presses Return

## Limitations

- macOS only
- Images and stickers appear as `圖片` / `貼圖` in copied text
- Chat history copy is capped at ~50KB (truncated from the beginning for very long chats)
- `send!` sends immediately — use with caution

## Acknowledgements

Inspired by [dtwang/line-desktop-mcp](https://github.com/dtwang/line-desktop-mcp), which pioneered the approach of controlling LINE desktop via GUI automation. This skill adapts the same AppleScript technique into a lightweight Claude Code skill that requires no persistent MCP server process.
