# AskEditor

Edit and make videos in [AskEditor](https://askeditor.com) from Claude, with the editor open beside
the chat. Ask for a cut, captions, music, titles, a hook or a motion graphic, and watch the timeline
change in front of you. You can adjust anything by hand at any time, and every change is saved to
your AskEditor project.

## What you need

- An AskEditor account. The free plan works.
- The Claude desktop app. The editor opens beside the chat in its Code tab. On the web and the phone
  the tools work too, and Claude gives you a link to the editor instead.

## Getting started

1. Install the plugin, then start a new session in the Code tab. In Claude Code you can also
   install it in one step:

   ```
   /plugin install askeditor --marketplace AskEditor/askeditor-plugin
   ```

2. Type `/mcp`, choose **askeditor** and press **Connect**. An AskEditor page names the account it
   will use; press **Allow**. There is no key or password to copy.
3. Say: *Open my latest AskEditor project beside this chat.*

## What it connects to, and what it sends

- **One server: AskEditor's own**, at `https://mcp.askeditor.com/mcp`, signed in with OAuth. It
  receives the requests Claude makes for you: which project to open, the edits to make, and the text
  you ask for.
- **The editor**, opened from `askeditor.com` in Claude's built-in browser pane, signed in for that
  project only.
- **Files, only when you ask.** A file from your computer is uploaded only when you ask Claude to
  bring it in: Claude runs the upload command AskEditor gives it, which sends that one file straight
  to AskEditor's own file storage over one-time https links issued for that upload. Footage you add
  in the editor stays on your computer until you choose Upload in the editor.
- The plugin installs nothing that runs by itself: no hooks, no scripts and no local server.

## What it costs

Editing is free: the timeline, text, motion graphics, captions you bring, looking at the edit and
exporting. Paid work, such as generation, voices and AskEditor's own transcription, uses AskEditor
credits, and anything that costs more than a little, or deletes something, asks you first.

## Your data

Your account, projects and uploaded media are kept by AskEditor until you delete them or your
account. See the [privacy policy](https://askeditor.com/privacy-policy) and the
[terms](https://askeditor.com/terms-of-service). Help: [askeditor.com/contact](https://askeditor.com/contact).
To disconnect Claude, revoke it under **Settings › API keys** in AskEditor.

## Licence

MIT. See `LICENSE`.
