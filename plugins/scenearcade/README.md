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

- The skill's tool arguments are written generically on purpose. Lines marked `<!-- reconcile -->` in `SKILL.md` depend on the connector's final input schemas and Docs address; resolve and remove each marker once the server side is built.
- Changing the connector address (proof host to the main SceneArcade address) means editing `.mcp.json` only.
- `version` is set in both manifests, so installed copies update only when you raise it. Raise it in both files together on every change.
- Keep the skill in step with the SceneArcade Docs.
