# Leaf Arcade agent skill

Play private board and card games with a human through the [Leaf Arcade CLI](https://www.npmjs.com/package/@leafarcade/cli). The human uses the browser; their agent uses the terminal. Supports 53 multiplayer games, including chess, Connect Four, Bridge and other games with multiple seats.

Add the skill to Claude Code, Codex, Cursor and other agents that read `SKILL.md`:

```sh
npx skills add leafarcade/skills
```

Or install the CLI and its bundled skill:

```sh
npm install -g @leafarcade/cli@latest
leafarcade skill install --agent codex
# Or: leafarcade skill install --agent claude
```

The skill install is explicit and offline. Existing customized skills are preserved; add `--update` to replace an older copy after the CLI backs it up outside the skills directory. Refresh your agent's skills and ask it to play Leaf Arcade. You can also copy `skills/leafarcade/` into your agent's skills directory manually.

Start from the agent's terminal:

```sh
leafarcade game create --game connect-four --name "My agent" --open
```

The agent hosts the room and the human joins through the returned browser URL. The agent waits for the join, starts the match, then plays each turn with `game play ... --wait --brief`, which moves and waits for the next turn and returns only the fields needed for the next decision (`--brief` requires CLI 0.6.0 or newer). CLI 0.7.0 adds complete legal move lists for most games (`legal_wire_actions`), readable card names (`cards_labeled`), labeled index boards and `changed_since_last_read`, which the skill relies on. Every JSON response includes `next`, the exact command to run next, so the agent never has to ask the human to report moves. In sandboxed agents (Codex, Claude Code), run the CLI with network access. The skill explains seat privacy, action conventions, waiting, rate limits and safe recovery from uncertain commands.

## Automatic local play

After joining and starting the match, choose your installed, logged-in agent:

```sh
leafarcade watch --room ROOMCODE --agent claude
# Or:
leafarcade watch --room ROOMCODE --agent codex
```

Watcher support requires CLI 0.2.0 or newer. Run the install command above again
to update. Other agents can use `--agent-command` with the documented JSON
adapter protocol. Keep the terminal and computer running. Defaults are one hour,
100 decisions and 120 seconds per decision; pause, finish, errors or Ctrl+C stop
the watcher without resigning. Model calls use your own provider allowance.

The watcher starts fresh local decisions rather than resuming an existing chat.
Use one watcher per seat. Read game status after an uncertain move; a checkpoint
prevents the same revision from being attempted again unless you explicitly
choose `--retry-current` after inspecting the state.

To update an existing installed skill, run
`leafarcade skill install --agent codex --update` (or `--agent claude`). The
installer moves the previous copy to `leafarcade-skill-backups/` outside the
skills directory and installs the bundled version. Without `--update` it keeps a
customized copy unchanged. Refresh the agent's skills.

## Releases

[GitHub Releases](https://github.com/leafarcade/skills/releases) track meaningful
changes to the skill. Tags match the CLI release that introduces the documented
behavior, such as `v0.2.0` for local watcher support. CLI-only patches and minor
README corrections do not need an empty skill release. Installation examples
continue to use `@latest`; release notes record exact compatibility versions.

This repository contains only skill instructions and metadata. CLI source stays in its private repository; the npm JavaScript executable is public. No model keys, accounts or hosted inference are required by the skill or CLI. Private rooms consume the game's service budget; agent model usage follows your own provider plan.

[Games and setup](https://leafarcade.com/play-with-ai/) · [npm package](https://www.npmjs.com/package/@leafarcade/cli) · [Skill instructions](skills/leafarcade/SKILL.md)
