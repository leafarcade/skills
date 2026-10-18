# Leaf Arcade agent skill

Play private board and card games with a human through the [Leaf Arcade CLI](https://www.npmjs.com/package/@leafarcade/cli). The human uses the browser; their agent uses the terminal. Supports 47 multiplayer games, including chess, Connect Four, Bridge and other games with multiple seats.

Install the CLI and its bundled skill:

```sh
npm install -g @leafarcade/cli@latest
leafarcade skill install --agent codex
# Or: leafarcade skill install --agent claude
```

The skill install is explicit and offline. Existing customized skills are preserved. Refresh your agent's skills and ask it to play Leaf Arcade. You can also copy `skills/leafarcade/` into your agent's skills directory manually.

Start from the agent's terminal:

```sh
leafarcade game create --game connect-four --name "My agent" --open
```

The agent hosts the room and the human joins through the returned browser URL. Once everyone is ready, the agent reads status and starts with the current revision. The skill explains seat privacy, action conventions, waiting, rate limits and safe recovery from uncertain commands.

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

To update an existing installed skill, back it up first. The installer preserves
customized or older instructions rather than overwriting them. Copy the reviewed
files from `skills/leafarcade/` into the existing skill directory, or remove that
backed-up directory and run `skill install` again. Refresh the agent's skills.

## Releases

[GitHub Releases](https://github.com/leafarcade/skills/releases) track meaningful
changes to the skill. Tags match the CLI release that introduces the documented
behavior, such as `v0.2.0` for local watcher support. CLI-only patches and minor
README corrections do not need an empty skill release. Installation examples
continue to use `@latest`; release notes record exact compatibility versions.

This repository contains only skill instructions and metadata. CLI source stays in its private repository; the npm JavaScript executable is public. No model keys, accounts or hosted inference are required by the skill or CLI. Private rooms consume the game's service budget; agent model usage follows your own provider plan.

[Games and setup](https://leafarcade.com/play-with-ai/) · [npm package](https://www.npmjs.com/package/@leafarcade/cli) · [Skill instructions](skills/leafarcade/SKILL.md)
