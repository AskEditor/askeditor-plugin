---
name: askeditor
description: Edit and make videos in AskEditor from this chat, with the editor open beside it. Use whenever the person tags @askeditor, mentions AskEditor, or asks to edit, cut, trim, caption, subtitle, add music, voice, titles, hooks or motion graphics to a video, to make a video from footage or a script, or to open, watch or export an AskEditor project.
---

# AskEditor beside this chat

AskEditor is a video editor on the web. You edit a project with the AskEditor tools (the `askeditor` server this plugin connects), and the person watches the same project in the editor, open in the browser pane beside this chat. Every change you make appears there by itself within a second or two.

**When the person tags AskEditor**, by typing `@askeditor` or `@AskEditor` or with a plugin mention whose link begins `plugin://askeditor`, the request is for AskEditor and nothing else. Open the project beside the chat and do the work with the AskEditor tools. Never answer a tagged request with another video tool, another editor plugin or a command on this computer, unless they ask for that or agree to it.

## 1. Connect

The AskEditor tools appear once the plugin is installed and the person has signed in. If they are missing, or a call answers that you must sign in, ask the person to connect AskEditor: open Plugins, choose AskEditor and sign in (in a terminal, `codex mcp login askeditor`). Their browser opens an AskEditor page, and they press Allow. Tools load when a task starts, so after a first install they start a new task.

Never ask the person for an API key, a password or a cookie, and never put one in a command.

## 2. Always show the editor before you edit

**Every time you work on a project, the editor is open beside the chat first.** It does not matter what the person asked for or whether they said "open": adding a graphic, cutting, captions, music, uploading a file to work on. Editing with nothing showing is a mistake, because watching the edit is why they installed this. If a tool's answer begins with `show_editor`, nobody can see the project: do what it says before anything else.

1. Work in the project the person opened or named: find it with `list_projects`. When they name a project, pass `search` with words from its title: the plain list holds only the newest fifty. Never look for a project by browsing AskEditor's pages. Then `open_project` to read its timeline. One project holds everything for a film, the pictures and video you generate as well as the cut, so never make a second project for it. Make a new one with `create_editor_project` only when they ask for a new project or have none; when you are not sure, ask.
2. Call `get_editor_url` with `pane: true`. It answers with the project's links:
   - `browser_handoff.url`, when it is there: a one-time link that opens the editor in the pane already signed in. It works once, for two minutes. Use it only to open the pane. Never show it, quote it or save it.
   - `pane_url`: the same editor with its own chat closed, made for the pane.
   - `url`: the ordinary link. This is the only one you ever show the person.
3. Open the pane on `browser_handoff.url` if there is one, otherwise on `pane_url`. These are the only addresses you ever open in the pane: never AskEditor's front page, and never an address you put together yourself, because only the link from this tool signs the pane in:
   - The pane is this app's in-app Browser. Control it the way the Browser plugin's own skill says (`control-in-app-browser`), and choose the in-app browser, `agent.browsers.get("iab")`, not Chrome: the person installed this plugin to watch the editor beside the chat.
   - Open one tab on the link, and show the browser so they can watch: `await (await iab.capabilities.get("visibility")).set(true)`.
   - **Keep the tab open.** This app closes a tab you opened when your turn ends, and the editor would vanish from beside the chat. So call `await tab.markDeliverable()` on the editor's tab as soon as it has loaded. The mark lasts one turn: call it again before you finish every later turn of this conversation, whether or not you touched the browser in that turn.
   - On a later turn, find that tab again with `iab.tabs.list()` and reuse it. Send it to anything new: a fresh one-time link, or another project. Do not open a second tab for the same project. If the tab is gone, call `get_editor_url` with `pane: true` again, open a new one, show the browser and mark it.
   - If the app asks the person to allow askeditor.com, wait for their answer. If it is refused, tell them, give them `url` and carry on. Do not retry in a loop.
   - If there is no in-app Browser, as in a terminal session, give the person `url` once and carry on editing. They can watch in their own browser.
4. If the pane shows AskEditor's front page or its sign-in page, it is not signed in: call `get_editor_url` with `pane: true` again and send the same tab to the fresh `browser_handoff.url`. Only when there is no `browser_handoff` does the person sign in there by hand, once. It is their account: do not type for them.
5. When a project has no pane link (`pane_url` is null): give the person `url` and carry on.

Open the pane once for a project. It updates by itself, so never reload it and never open a second tab for the same project. At the start of each later turn, make sure it is still showing; if it has gone, open it again the same way before you edit.

## 3. Edit with the tools, not by clicking

Change the project only through the AskEditor tools. Do not click, type or drag in the editor's page to make an edit: the tools are exact, and the page is for the person to watch and to adjust by hand. Because they may have adjusted something, read the timeline again (`open_project` or `get_timeline`) before changing a clip you last saw a while ago.

Before any kind of work you have not done yet in this conversation, call `list_skills`, then `load_skill` for the guide that covers it: captions, sound, motion graphics, hooks, title cards, talking videos and more. The guides are AskEditor's own and are kept current on the server. Follow them over your own habits.

After each change that can be seen, look at it with `watch_edit`, which returns the edit as pictures, as it will export, before you say it is done. A screenshot of the pane is not proof.

Do the work yourself with the tools. Call `ask_askeditor` only when the person asks for AskEditor's own agent: it is billed as a chat turn on their AskEditor account.

## 4. What costs, and what cannot be undone

A call that spends more than a few credits, or deletes something, waits for the person. If this app shows them a dialog, wait for their answer. If the tool answers `needs_approval`, tell the person what it is and what it costs, and ask them to approve it in AskEditor in their own browser, with the link in that answer: the pane beside this chat cannot approve. Then call the tool again with the `approval_id`. If they decline, stop.

Never call `export_video` unless the person asks for the finished file.

## 5. Files from this computer

To bring in footage, pictures or audio from the person's machine: `create_upload`, send each part with the command it gives, then `complete_upload`, which can place the file on the timeline. From a web address: `import_media_from_url`.

<!-- Generated. Edit skill/ and run scripts/agent-plugin/build.mjs. -->
