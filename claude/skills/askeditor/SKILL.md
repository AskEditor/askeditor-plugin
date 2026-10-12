---
name: askeditor
description: Edit and make videos in AskEditor from this chat, with the editor open beside it. Use whenever the person tags @askeditor, mentions AskEditor, or asks to edit, cut, trim, caption, subtitle, add music, voice, titles, hooks or motion graphics to a video, to make a video from footage or a script, or to open, watch or export an AskEditor project.
---

# AskEditor beside this chat

AskEditor is a video editor on the web. You edit a project with the AskEditor tools (the `askeditor` server this plugin connects), and the person watches the same project in the editor, open in the browser pane beside this chat. Every change you make appears there by itself within a second or two.

**When the person tags AskEditor**, by typing `@askeditor` or `@AskEditor` or with a plugin mention whose link begins `plugin://askeditor`, the request is for AskEditor and nothing else. Open the project beside the chat and do the work with the AskEditor tools. Never answer a tagged request with another video tool, another editor plugin or a command on this computer, unless they ask for that or agree to it.

## 1. Connect

The AskEditor tools appear once the plugin is installed and the person has signed in. If they are missing, or a call answers that you must sign in, ask the person to connect AskEditor: type `/mcp`, choose `askeditor` and press Authenticate (in a terminal, `claude mcp login plugin:askeditor:askeditor`). Their browser opens an AskEditor page, and they press Allow. Tools load when a session starts, so after a first install they start a new session.

Never ask the person for an API key, a password or a cookie, and never put one in a command.

## 2. Always show the editor before you edit

**Every time you work on a project, the editor is open beside the chat first.** It does not matter what the person asked for or whether they said "open": adding a graphic, cutting, captions, music, uploading a file to work on. Editing with nothing showing is a mistake, because watching the edit is why they installed this. If a tool's answer begins with `show_editor`, nobody can see the project: do what it says before anything else.

1. Work in the project the person opened or named: find it with `list_projects`. When they name a project, pass `search` with words from its title: the plain list holds only the newest fifty. Never look for a project by browsing AskEditor's pages. Then `open_project` to read its timeline. One project holds everything for a film, the pictures and video you generate as well as the cut, so never make a second project for it. Make a new one with `create_editor_project` only when they ask for a new project or have none; when you are not sure, ask.
2. Call `get_editor_url` with `pane: true`. It answers with the project's links:
   - `browser_handoff.url`, when it is there: a one-time link that opens the editor in the pane already signed in. It works once, for two minutes. Use it only to open the pane. Never show it, quote it or save it.
   - `pane_url`: the same editor with its own chat closed, made for the pane.
   - `url`: the ordinary link. This is the only one you ever show the person.
3. Open the pane on `browser_handoff.url` if there is one, otherwise on `pane_url`. These are the only addresses you ever open in the pane: never AskEditor's front page, and never an address you put together yourself, because only the link from this tool signs the pane in:
   - The pane is the Claude desktop app's built-in browser. Its tools are named `mcp__Claude_Browser__…`. If they are not in your tool list, load them all in one ToolSearch call with the query `mcp__Claude_Browser__`.
   - Open the link with `preview_start` and its `url`. It opens a new tab and returns a `tabId`. Keep that id, and use `navigate` with it for anything later: a fresh one-time link, or another project. Do not call `preview_start` again for the same project.
   - The first time, the app may ask the person to allow askeditor.com. Wait for their answer. If it is refused, tell them, give them `url` and carry on. Do not retry in a loop.
   - Before you tell the person to look at the pane or do something in it, call `tabs_context`, which says whether the pane is showing. If it is hidden, ask them to press Cmd+Shift+B (Ctrl+Shift+B on Windows).
   - If there are no built-in browser tools at all, as in a terminal session, give the person `url` once and carry on editing. They can watch in their own browser.
4. If the pane shows AskEditor's front page or its sign-in page, it is not signed in: call `get_editor_url` with `pane: true` again and send the same tab to the fresh `browser_handoff.url`. Only when there is no `browser_handoff` does the person sign in there by hand, once. It is their account: do not type for them.
5. When a project has no pane link (`pane_url` is null): give the person `url` and carry on.

Open the pane once for a project. It updates by itself, so never reload it and never open a second tab for the same project. At the start of each later turn, make sure it is still showing; if it has gone, open it again the same way before you edit.

## 3. Edit with the tools, not by clicking

Change the project only through the AskEditor tools. Do not click, type or drag in the editor's page to make an edit: the tools are exact, and the page is for the person to watch and to adjust by hand. Because they may have adjusted something, read the timeline again (`open_project` or `get_timeline`) before changing a clip you last saw a while ago.

Before any kind of work you have not done yet in this conversation, call `list_skills`, then `load_skill` for the guide that covers it: captions, sound, motion graphics, hooks, title cards, talking videos and more. The guides are AskEditor's own and are kept current on the server. Follow them over your own habits.

After each change that can be seen, look at it with `watch_edit`, which returns the edit as pictures, as it will export, before you say it is done. A screenshot of the pane is not proof.

Do the work yourself with the tools. Call `ask_askeditor` only when the person asks for AskEditor's own agent: it is billed as a chat turn on their AskEditor account.

## 4. What is free, and what uses credits

AskEditor is free to edit with. Everything on the timeline, text, motion graphics, styling and importing captions, bringing media in, looking at the edit and exporting use no credits. Reading what a clip says with its times (`get_clip_transcript`, which is how you know where to cut), removing pauses (`tighten_silences`), cutting a person out of the background (`cut_out_person`), and the effects and hooks that use that cut-out (`apply_tracking_effect`, `add_hook`) are free too, up to 300 credits' worth a day; past that they use credits like any other paid tool. Tools that generate (pictures, video, voices, music, captions written by AskEditor's own transcriber) and AskEditor's own agent use the person's AskEditor credits, on any plan, Free included.

`open_project` says how many credits there are. Every plan keeps files in AskEditor cloud, so on any plan you can bring a file in yourself (`create_upload`, `import_media_from_url`) and export with `export_video`. The Free plan keeps up to 2 GB there, 500 MB a file. When a tool answers that a file is too big or that there is no room, say so plainly: the person can delete files in AskEditor's Assets to make room, or add the file in the editor themselves, where it stays on their own computer and costs nothing. If they want more room than the Free plan has, the paid plans keep more: give them https://askeditor.com/pricing as a link they can press, which opens in their own browser. Never open it in the pane or in a tab of your own, and never choose a plan or pay for them.

When the person would rather not spend credits on something, offer the free way: make it with a tool this app already has (a voice, a picture, music), then bring it in with `import_media_from_url` or `create_upload`. For captions, read the words with `get_clip_transcript` and put them on with `import_captions`.

Do not render a motion graphic just to show it: the editor shows it live and the export draws it.

## 5. What costs, and what cannot be undone

A call that spends more than a few credits, or deletes something, waits for the person. If this app shows them a dialog, wait for their answer. If the tool answers `needs_approval`, tell the person what it is and what it costs, and ask them to press Approve on the line under the header of the editor open beside this chat (or on the card in AskEditor in their own browser, with the link in that answer). When they say they have, or the line has gone from the editor, call the tool again with the same arguments and the `approval_id`: do not wait for anything else. If they decline, stop.

If a tool answers `waiting_for_credits`, nothing ran and nothing was charged: the person's AskEditor balance cannot cover it. Tell them in one plain sentence how many more credits it needs and where to add them, as the answer says. The answer gives an address that adds the credits. Give it to them as a link they can press: it opens in their own browser, on the pack that covers it, and they pay there. Never open it in the pane or in a tab of your own, and never pay for them. The editor beside this chat says the same under its header, and its Copy link copies the same address. Then call `wait_for_credits` with the `hold_id`. It returns when the credits are there, within ten minutes; then call the tool again with the same arguments. If it returns `covered: false`, say so and stop. Never name a tool to the person, and never say they must buy credits to edit: everything on the timeline is free.

Never call `export_video` unless the person asks for the finished file.

## 6. Files from this computer

To bring in footage, pictures or audio from the person's machine: `create_upload`, send each part with the command it gives, then `complete_upload`, which can place the file on the timeline. From a web address: `import_media_from_url`.

### Where the person's files are kept

The editor has two places for the files a person adds, and the button beside Export says which one is in use. Use the same two names when you talk about it, never "local mode" or "the server":

- **This computer**, the default on every plan. Nothing is uploaded: the files stay in that browser and the film is exported there.
- **AskEditor cloud**, on every plan (the Free plan keeps up to 2 GB there, 500 MB a file). It lets the person open the project on any computer or phone, lets you watch, transcribe and cut out their footage, keeps the files safe if the browser's data is cleared, and gives them share links, reels and scheduled posts.

The project and its timeline are always saved on AskEditor whichever place is chosen, which is why you can edit either kind of clip. When the person asks what the choice means, or a tool is refused because a file is only on their computer, say it in those words, and tell them the button beside Export opens a panel that shows both places.

### A file that is only on the person's computer

A file added while the place is This computer is never uploaded. That is AskEditor's privacy promise, not a fault: the person's footage stays on their computer until they choose to upload it, and **Upload all** in the editor is how they choose (the "only here" button beside the place chip at the top, or Exports on the left). Such a clip is on the timeline like any other, and you can cut, move, trim, style and caption it. What you cannot do is see or hear it: a tool that must read the file answers that it is only on the person's computer.

- Do not retry it, and do not try another tool to read the same file.
- Tell the person in plain words, and ask them what is in the footage if you need to know. If they want you to watch, transcribe or cut it out, tell them they can press Upload all, which keeps every clip and cut as it is; never upload it for them.
- `watch_edit` still shows the text, graphics and captions, and says which footage is missing from its pictures.
- Such a film is exported in the editor on that computer: the person presses Export there, free. `export_video` refuses it until they press Upload all.
- A file you bring in yourself (`create_upload`, `import_media_from_url`) is uploaded as always. Say so first if the person has told you they want nothing uploaded.

<!-- Generated. Edit skill/ and run scripts/agent-plugin/build.mjs. -->
