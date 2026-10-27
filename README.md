# SceneArcade plugins

**You don't need this plugin.** You can publish a finished browser game to SceneArcade from the AI app you already use by adding SceneArcade's connector to it. The plugin in this repository is an optional extra (see [The plugin](#the-plugin-optional)).

Only invited (proof) accounts can publish today. The connector points at SceneArcade's proof server, `https://proof.nex6.com/mcp`, until the main address is ready.

## Connect your app

### Claude (desktop app Code tab, and Claude Code)

1. Open this link: <https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=SceneArcade&connectorUrl=https%3A%2F%2Fproof.nex6.com%2Fmcp>
2. Press **Add**.
3. Sign in on SceneArcade's page.
4. Press **Approve**.

That reaches the Claude desktop app's **Code** tab and Claude Code.

#### Claude Code in a terminal (beta)

The terminal needs one extra step, even when the desktop app is already connected: run `/mcp`, pick **claude.ai SceneArcade** and choose **Authenticate**. Your browser opens; press **Approve**.

On Windows, if PowerShell blocks `claude`, run `claude.cmd` instead.

Having trouble? Email support@scenearcade.com.

### Codex (beta)

1. Open **Plugins**, then **MCPs**, then **Add**, then **Connect to a custom MCP**.
2. Choose **Streamable HTTP** first.
3. Name: `scenearcade`. URL: `https://proof.nex6.com/mcp`. Leave **Bearer token** and **Headers** empty.
4. **Save**, then **Restart**, then **Authenticate**, then **Approve**.

To change the type later, **Uninstall** the entry first and add it again.

Having trouble? Email support@scenearcade.com.

#### If Codex stops showing the SceneArcade tools, or doesn't offer to sign in

Codex's saved sign-in has probably expired, and reinstalling does not clear it. Run:

```text
codex mcp logout scenearcade
codex mcp login scenearcade
```

Approve in your browser, then restart Codex.

On Windows, `codex` may not be on your PATH. It is at `%LOCALAPPDATA%\OpenAI\Codex\bin\<folder>\codex.exe`.

### Which account is it?

Your SceneArcade account is whichever account your browser is signed in to on proof.nex6.com when you approve. Check the name on the approval page.

## What you need

- One of the apps above, running on your own computer (Windows, macOS or Linux). Publishing sends your game's ZIP file with one command, so the app needs a command line: the Claude desktop app's Code tab, Claude Code, or Codex. It does not work from the Claude desktop **chat** tab, claude.ai, ChatGPT chat or any website.
- An invited SceneArcade (proof) account.
- A finished browser game.

## Publish a game

Open your game's folder in the app and say: **"Publish this game to SceneArcade."**

The assistant then:

1. Confirms which SceneArcade account is connected, and asks you for the listing details it can't know (title, type, phone support, whether you are still developing it, which AI models built it, and whether you want the One Shot label).
2. Packs the game into a ZIP with the required cover image.
3. Play-tests it and writes the testing report.
4. Sends the details and the ZIP's size and fingerprint to SceneArcade (**approval 1**: your app asks you to approve `submit_build`), and gets back a one-time upload address.
5. Uploads the ZIP with one command (**approval 2**: your app asks you to approve that command). Some apps' automatic safety modes may refuse an upload to an outside address; if yours does, the assistant will tell you what it said.
6. Checks the status and tells you what SceneArcade found.

You get two approval prompts: the submit, then the upload.

Your game file goes straight into your private storage on SceneArcade. It never passes through the AI's context, and the assistant sends only the packed ZIP.

## The plugin (optional)

The plugin adds the same publishing guide as a skill (`/scenearcade:publish` in Claude Code), so the assistant has the steps ready from the start. The connector already carries the same guide, so the plugin is a convenience, not a requirement.

1. Add the SceneArcade list and install the plugin.

   Claude Code, terminal:

   ```text
   claude plugin marketplace add Maathony/scenearcade-plugins
   claude plugin install scenearcade@scenearcade-plugins
   ```

   Or, inside a Claude Code session:

   ```text
   /plugin marketplace add Maathony/scenearcade-plugins
   /plugin install scenearcade@scenearcade-plugins
   ```

   Codex, terminal:

   ```text
   codex plugin marketplace add Maathony/scenearcade-plugins
   codex plugin add scenearcade@scenearcade-plugins
   ```

   The Claude desktop app's Code tab and the Codex app use the same plugin settings as their terminals: add the list once with the terminal command, restart the app, then install **SceneArcade** from its plugins screen. Plugins are not available in cloud or WSL sessions of the Claude desktop app.

2. Restart the app, or run `/reload-plugins` in Claude Code. Bundled skills and tools appear in new sessions only.
3. The plugin carries its own copy of the connector address. If your app asks you to sign in again for it, do so (in Claude Code: `/mcp`, pick `plugin:scenearcade:publisher`, **Authenticate**) and press **Approve**.

## What is in here

- `.claude-plugin/marketplace.json`: the list Claude Code reads.
- `.agents/plugins/marketplace.json`: the list Codex reads.
- `plugins/scenearcade/`: the plugin itself (see its [README](plugins/scenearcade/README.md)).

The plugin holds no secrets: an address, and the publishing instructions the assistant follows. Your sign-in is kept by your app.

## Licence

[MIT](LICENSE)
