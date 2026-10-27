# SceneArcade plugin

**You don't need this plugin.** Adding SceneArcade's connector to Claude or Codex is enough to publish a finished browser game; the one-click Claude link and the Codex custom-MCP steps are in the [repository README](../../README.md). Only invited (proof) accounts can publish today.

To add it anyway (Claude Code):

```text
claude plugin marketplace add Maathony/scenearcade-plugins
claude plugin install scenearcade@scenearcade-plugins
```

Codex and the desktop apps: see "The plugin (optional)" in the repository README.

## What it adds

The plugin is an optional extra: the same publishing guide as a skill.

- **`publish` skill** (`skills/publish/SKILL.md`): the steps the assistant follows. It is a condensed copy of the guide the connector itself carries: pack the ZIP with its cover, play-test it, write the testing report, work out the size and SHA-256, call `submit_build` (approval 1), upload with one `curl` command (approval 2), then call `get_submission`. In Claude Code it runs as `/scenearcade:publish`; the assistant also picks it up when you ask to publish a game.
- **`publisher` connector** (`.mcp.json`): the same remote MCP server the connector link adds, at `https://proof.nex6.com/mcp`, with three tools: `get_account`, `submit_build` and `get_submission`. If your app asks you to sign in for it, sign in once in your browser and press **Approve**.

Your SceneArcade account is whichever account your browser is signed in to on proof.nex6.com when you approve. Check the name on the approval page.

## Files

```text
plugins/scenearcade/
  .claude-plugin/plugin.json   Claude Code manifest
  .codex-plugin/plugin.json    Codex manifest
  .mcp.json                    the connector (shared by both apps)
  skills/publish/SKILL.md      the publishing skill (shared by both apps)
  README.md
```

## Maintainers

- The connector's tool schemas and replies, and the `guide` that `get_account` returns (`app/mcp/guide.ts` in the platform repo), are the source of truth. `SKILL.md` follows them; when they differ, the connector wins. The SceneArcade Docs are background.
- Moving from the proof host to the main SceneArcade address means editing `.mcp.json` and the two `proof.nex6.com` Docs addresses in `SKILL.md` (the intro and the `instructionsUrl` example).
- `version` is set in both manifests, so installed copies update only when you raise it. Raise it in both files together on every change.
