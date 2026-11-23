# poteto-lite

A cheap, in-chat version of the `poteto-mode` skill for Claude Code.

## About

[pstack](https://github.com/cursor/plugins/tree/main/pstack) ships a skill called `poteto-mode`. It gives an agent good habits: name the data first, make the smallest change, trace bugs to their root cause, and prove the result on the real thing. It also runs a heavy process. It reads about 55 KB of instructions before any work, hands steps to helper agents that each reread the main file, and runs a multi-model review before a PR.

On a small Claude plan that adds up. `poteto-lite` keeps the habits, a short design and build flow, and the cleanup steps, and drops the machinery. It runs entirely in the current chat. It starts no subagents, runs no review panel, and reads no playbooks.

## What it does

- **Habits.** Data shape first, smallest change, root cause for bugs, proof on the real artifact, no needless questions on reversible work.
- **Flow.** Understand, design, build, prove, cleanup, reply. Each phase runs in the chat and is skipped when it has nothing to act on. Design picks one of two written approaches and asks only when the choice is hard to undo. Build writes the failing test first for a bug.
- **Cleanup before finishing.** Runs `deslop` on the diff, does a comment pass in the chat, and runs `unslop` on any prose it wrote.
- **Plain replies.** Short sentences, claims labeled measured, inferred or guess, and no invented links or results.
- **Escalation.** When a task touches many files, needs a hard-to-undo design choice, or has a bug with no known cause, it stops, says so, and suggests `poteto-mode`. It never escalates on its own.

## Installation

### Requirements

- An agent that reads `SKILL.md` skills: Claude Code, Cursor, or Antigravity
- Optional: the [t3-pstack](https://github.com/chhoumann/t3-pstack) plugin on Claude Code. Its `t3-pstack:deslop` and `t3-pstack:unslop` skills run the cleanup steps. Without them, the skill applies short built-in versions of the same rules.

### Install

Clone it once, then link it into each tool's skills folder.

```bash
git clone https://github.com/Heritsam/poteto-lite ~/.agents/skills/poteto-lite
ln -s ~/.agents/skills/poteto-lite ~/.claude/skills/poteto-lite                     # Claude Code
ln -s ~/.agents/skills/poteto-lite ~/.cursor/skills/poteto-lite                     # Cursor
mkdir -p ~/.gemini/antigravity-cli/skills
ln -s ~/.agents/skills/poteto-lite ~/.gemini/antigravity-cli/skills/poteto-lite     # Antigravity (agy and T3 Code)
```

Link only the tools you use. Restart the tool, or reload its skills, so `poteto-lite` appears.

## Usage

```
/poteto-lite fix the sorting bug in the table component
```

Use it for small or medium changes, a bug with an obvious cause, or a question about code. Switch to the full skill when a task is big:

```
/t3-pstack:poteto-mode migrate the auth layer to the new session API
```

## poteto-lite and poteto-mode

| | `poteto-mode` | `poteto-lite` |
|---|---|---|
| Who does the work | Helper agents on configured models | The current chat |
| Reads first | About 55 KB, then a playbook | Nothing extra |
| Review | Multi-model panel before a PR | None unless you ask |
| PRs | Links, watches and babysits them | None |
| Design and build | Playbooks per task type, delegated | One short inline flow for bugs, features and refactors |
| Cleanup | deslop, no-comments and unslop through helpers | The same three steps, run in the chat |
| Cost | High | Close to a normal chat |

## Limits

- I have only run the Cursor and Antigravity setup as far as creating the links. I have not confirmed either tool loads the skill, so treat those two as untested.
- I wrote this from reading `poteto-mode`. It is a summary, not a copy, and I have not yet run it on a long task.
- It reads no playbooks. Its flow is a one-line summary of each, so it only partly copies their discipline, such as committing the failing test before the fix.
- Its comment pass is lighter than the `no-comments` skill, which uses a separate reviewer agent. Run `/t3-pstack:no-comments` when you want that.

## Credits

`poteto-mode` and pstack are by Lauren Tan. The Claude Code port is by Michael Denyer, and the T3 Code port is [chhoumann/t3-pstack](https://github.com/chhoumann/t3-pstack). This repository is an independent, unofficial companion and is not affiliated with them.

## License

MIT. See [`LICENSE`](LICENSE).
