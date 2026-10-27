# SceneArcade plugin

Lets Claude Code and Codex publish a finished browser game to SceneArcade. Setup steps are in the [repository README](../../README.md).

## What it adds

- **`publisher` connector** (`.mcp.json`): a remote MCP server at `https://proof.nex6.com/mcp` with three tools: `get_account`, `submit_build` and `get_submission`. In Claude Code they appear as `mcp__plugin_scenearcade_publisher__<tool>`. You sign in once in your browser.
- **`publish` skill** (`skills/publish/SKILL.md`): the steps the assistant follows. It is a condensed copy of SceneArcade's Docs pages "Prepare and test" and "Connect and publish", rewritten for this flow: pack the ZIP with its cover, play-test it, write the testing report, work out the size and SHA-256, call `submit_build`, upload with one `curl` command, then call `get_submission`.

In Claude Code the skill runs as `/scenearcade:publish`; the assistant also picks it up when you ask to publish a game.

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

- `SKILL.md` was reconciled with the connector code (`app/mcp/route.ts` in the platform repo, branch `feat/ip9a-connector`). If a tool's input or reply changes, update the skill; the tool's own schema wins where they differ.
- Moving from the proof host to the main SceneArcade address means editing `.mcp.json` and the two `proof.nex6.com` Docs addresses in `SKILL.md` (the intro and the `instructionsUrl` example).
- `version` is set in both manifests, so installed copies update only when you raise it. Raise it in both files together on every change.
- Keep the skill in step with the SceneArcade Docs.
