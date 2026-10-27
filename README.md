# SceneArcade plugins

Publish a finished browser game to SceneArcade from the AI app you already use: Claude Code or Codex.

This is an early proof. It works for invited SceneArcade preview accounts only, and the plugin points at SceneArcade's proof server (`https://proof.nex6.com/mcp`) until the main address is ready.

## What you need

- Claude Code (terminal, or the Code tab of the Claude desktop app) or Codex (terminal or app), running on your own computer: Windows, macOS or Linux.
- A SceneArcade preview account.
- A finished browser game.

It does not work from the Claude desktop **chat** tab, claude.ai, ChatGPT chat or any website. Those have no command line, and publishing needs one to send your game's ZIP file.

## Set up (about two minutes, once per app)

### Claude Code, terminal

1. Add the SceneArcade list and install the plugin:

   ```text
   claude plugin marketplace add Maathony/scenearcade-plugins
   claude plugin install scenearcade@scenearcade-plugins
   ```

   Or, inside a Claude Code session:

   ```text
   /plugin marketplace add Maathony/scenearcade-plugins
   /plugin install scenearcade@scenearcade-plugins
   ```

2. Restart Claude Code, or run `/reload-plugins`.
3. Sign in. Run `/mcp`, pick the SceneArcade server (`plugin:scenearcade:publisher`) and choose **Authenticate**. Your browser opens: sign in to SceneArcade and press **Approve**. Claude Code remembers the connection.

### Claude desktop app, Code tab

1. Open a local session in the **Code** tab. Click **+** next to the prompt box, then **Add plugins**.
2. Add the list `Maathony/scenearcade-plugins` and install **SceneArcade**. If the plugin browser has no way to add a list, run the two terminal commands above once; the desktop app uses the same plugin settings as the terminal.
3. Start a new session and ask: "Check my SceneArcade account." When your browser opens, sign in and press **Approve**.

Plugins are not available in cloud or WSL sessions of the desktop app.

### Codex, terminal

1. Add the SceneArcade list and install the plugin:

   ```text
   codex plugin marketplace add Maathony/scenearcade-plugins
   codex plugin add scenearcade@scenearcade-plugins
   ```

   Or run `codex`, type `/plugins`, open the SceneArcade list and install **SceneArcade**.
2. Start a new session (bundled skills and tools appear in new sessions only).
3. Ask: "Check my SceneArcade account." When your browser opens, sign in and press **Approve**.

### Codex, app

1. Add the list once with the terminal command above (`codex plugin marketplace add Maathony/scenearcade-plugins`). The app and the terminal share this setting. Then restart the app.
2. Open the **Plugins** tab, choose the **SceneArcade** list and install **SceneArcade**.
3. Start a new chat and ask: "Check my SceneArcade account." When your browser opens, sign in and press **Approve**.

## Publish a game

Open your game's folder in the app and say: **"Publish this game to SceneArcade."**

The assistant then:

1. Confirms which SceneArcade account is connected, and asks you for the listing details it can't know (title, type, phone support, whether you are still developing it, which AI models built it).
2. Packs the game into a ZIP with the required cover image.
3. Play-tests it and writes the testing report.
4. Sends the details and the ZIP's size and fingerprint to SceneArcade, and gets back a one-time upload address.
5. Uploads the ZIP with one command. **Your app asks you to approve that command. Approve it once.** Some apps' automatic safety modes may refuse an upload to an outside address; if yours does, the assistant will tell you what it said.
6. Checks the status and tells you what SceneArcade found.

Your game file goes straight into your private storage on SceneArcade. It never passes through the AI's context, and the assistant sends only the packed ZIP.

## What is in here

- `.claude-plugin/marketplace.json`: the list Claude Code reads.
- `.agents/plugins/marketplace.json`: the list Codex reads.
- `plugins/scenearcade/`: the plugin itself (see its [README](plugins/scenearcade/README.md)).

The plugin holds no secrets: an address, and the publishing instructions the assistant follows. Your sign-in is kept by your app.

## Licence

[MIT](LICENSE)
