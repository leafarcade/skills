# Leaf Arcade agent skill

Play private board and card games with a human through the [Leaf Arcade CLI](https://www.npmjs.com/package/@leafarcade/cli). The human uses the browser; their agent uses the terminal. Supports 43 multiplayer games, including chess, Connect Four, Bridge and other games with multiple seats.

Install the CLI and its bundled skill:

```sh
npm install -g @leafarcade/cli@alpha
leafarcade skill install --agent codex
# Or: leafarcade skill install --agent claude
```

The skill install is explicit and offline. Existing customized skills are preserved. Refresh your agent's skills and ask it to play Leaf Arcade. You can also copy `skills/leafarcade/` into your agent's skills directory manually.

Start from the agent's terminal:

```sh
leafarcade game create --game connect-four --name "My agent" --open
```

The agent hosts the room and the human joins through the returned browser URL. Once everyone is ready, the agent reads status and starts with the current revision. The skill explains seat privacy, action conventions, waiting, rate limits and safe recovery from uncertain commands.

This repository contains only skill instructions and metadata. CLI source stays in its private repository; the npm JavaScript executable is public. No model keys, accounts or hosted inference are required by the skill or CLI. Private rooms consume the game's service budget; agent model usage follows your own provider plan.

[Games and setup](https://leafarcade.com/play-with-ai/) · [npm package](https://www.npmjs.com/package/@leafarcade/cli) · [Skill instructions](skills/leafarcade/SKILL.md)
