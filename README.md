# AskEditor for ChatGPT and Claude

Edit and make videos in [AskEditor](https://askeditor.com) from the chat you already use, with the
editor open beside it. You ask in the chat; the timeline, the captions and the graphics change in
front of you, and you can adjust anything by hand at any time.

The thinking runs on your own ChatGPT or Claude plan. AskEditor credits are used only for paid
work such as generation, voices and renders, and anything that costs more than a little asks you
first.

## What you need

- An AskEditor account (the free plan works).
- The ChatGPT desktop app, or the Claude desktop app with a paid Claude plan. The web and phone
  apps have no browser pane; there the tools work and you are given a link to the editor.

## Install in the ChatGPT desktop app

Open **Plugins**, search for **AskEditor** and install it, then sign in when asked. From a terminal:

```
codex plugin marketplace add https://github.com/EbenKouao/askeditor-plugin.git
codex plugin add askeditor@askeditor
codex mcp login askeditor
```

Start a new task and say: *Open my latest AskEditor project beside this chat.*

## Install in Claude

In the Code tab, press **+**, choose **Plugins**, and install **AskEditor**. From a terminal:

```
claude plugin marketplace add https://github.com/EbenKouao/askeditor-plugin.git
claude plugin install askeditor@askeditor
claude mcp login plugin:askeditor:askeditor
```

Start a new session, pick the folder your footage is in, and say: *Open my latest AskEditor
project beside this chat.*

## Signing in

Your browser opens an AskEditor page that names the app asking, and you press **Allow**. There is
no key to copy. To disconnect an app later, revoke it under **Settings › API keys** in AskEditor.

## Updating

A plugin installed from Git does not update itself.

```
codex plugin marketplace upgrade askeditor
claude plugin marketplace update askeditor && claude plugin update askeditor@askeditor
```

## What is in here

| Path | What it is |
|---|---|
| `codex/` | The plugin for the ChatGPT desktop app: its manifest, the AskEditor connection and one skill |
| `claude/` | The same for Claude |
| `.agents/plugins/marketplace.json`, `.claude-plugin/marketplace.json` | What each app reads to find its plugin |

The skill only says how to connect and how to open the editor beside the chat. Everything about
editing well comes from AskEditor itself while you work, so it is always current.
