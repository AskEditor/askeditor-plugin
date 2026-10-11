# AskEditor for ChatGPT and Claude

Edit and make videos in [AskEditor](https://askeditor.com) from the chat you already use, with the
editor open beside it. You ask in the chat; the timeline, the captions and the graphics change in
front of you, and you can adjust anything by hand at any time.

The thinking runs on your own ChatGPT or Claude plan. AskEditor credits are used only for paid
work such as generation, voices and renders, and anything that costs more than a little asks you
first.

## What you need

- An AskEditor account (the free plan works).
- The Claude desktop app with a paid Claude plan, or the ChatGPT desktop app. The web and phone
  apps have no browser pane; there the tools work and you are given a link to the editor.

## Install in Claude

In the Claude desktop app, open **Customize**, then **Plugins**. Press **Add**, choose **Add from a
repository**, enter `EbenKouao/askeditor-plugin` and press **Sync**. Then install **AskEditor**.

From a terminal instead:

```
claude plugin marketplace add https://github.com/EbenKouao/askeditor-plugin.git
claude plugin install askeditor@askeditor
```

Open the **Code** tab and start a new session in the folder your footage is in. Type `/mcp`, choose
**askeditor** and press **Connect** (in a terminal, `claude mcp login plugin:askeditor:askeditor`).
Then say: *Open my latest AskEditor project beside this chat.*

## Install in the ChatGPT desktop app

From a terminal:

```
codex plugin marketplace add https://github.com/EbenKouao/askeditor-plugin.git
codex plugin add askeditor@askeditor
codex mcp login askeditor
```

Start a new task and say: *Open my latest AskEditor project beside this chat.*

## Signing in

Your browser opens an AskEditor page that names the app asking and the account it will use, and
you press **Allow**. There is no key to copy. To disconnect an app later, revoke it under
**Settings › API keys** in AskEditor.

## Updating

A plugin installed from a repository does not update itself.

```
claude plugin marketplace update askeditor && claude plugin update askeditor@askeditor
codex plugin marketplace upgrade askeditor
```

## What is in here

| Path | What it is |
|---|---|
| `claude/` | The plugin for Claude: its manifest, the AskEditor connection and one skill |
| `codex/` | The same for the ChatGPT desktop app |
| `.claude-plugin/marketplace.json`, `.agents/plugins/marketplace.json` | What each app reads to find its plugin |

The skill only says how to connect and how to open the editor beside the chat. Everything about
editing well comes from AskEditor itself while you work, so it is always current.
