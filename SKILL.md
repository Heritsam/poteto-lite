---
name: poteto-lite
description: Cheap version of poteto-mode. Use only when the user types /poteto-lite or asks for lite poteto. Same habits and cleanup steps, no subagents, no review panel, no big skill reads.
---

# Poteto lite

Work in this chat only. Start no subagents, no `delegate_task`, no panel review, and do not read `t3-pstack:poteto-mode` or its playbooks. Say so in one line if a step would normally have delegated.

## Habits kept from poteto-mode

- **Data first.** Name the data shape before writing logic.
- **Smallest change.** Delete before you add. No new abstraction for one caller.
- **Bug means root cause.** Reproduce it first, trace the symptom to its cause, fix it once where all callers route through.
- **Prove it.** Run the real artifact (test, CLI, app, page) and report what you ran. "It compiles" is not proof.
- **Don't block on the human.** On reversible work, pick a sensible default, do it, and say what you chose. Ask only for irreversible or product calls.
- **No comments** unless the code cannot show a non-obvious why.

## Cleanup before you finish

Run these in this chat. They are small, so they stay in lite.

1. **Code changed.** Run the `deslop` skill on the diff if your harness has one (`t3-pstack:deslop` on Claude Code). Otherwise apply its rules yourself. Remove comments that are unnecessary or off the local style. Remove defensive checks and try/catch that are abnormal for trusted code paths. Remove `any` casts used only to dodge type errors. Flatten deep nesting with early returns. Keep behavior unchanged and edits small.
2. **Comments.** Do the no-comments pass yourself. Read the diff for comments and delete each one that is not a non-obvious why the code cannot show. Do not spawn comment-sicko. For the full subagent version, the user types `/t3-pstack:no-comments`.
3. **Prose written.** Run the `unslop` skill (`t3-pstack:unslop` on Claude Code) on any doc, README, PR description, or commit message you wrote, and on your final reply when it runs longer than a few sentences. Without that skill, cut these yourself. AI vocabulary such as "additionally", "crucial", "delve", "pivotal" and "showcase". "Serves as" and "boasts" where "is" or "has" works. "Not just X, but Y". Em dashes, and colons used as mid-sentence connectors. Bold lead-ins that restate the line. Filler like "in order to" and "it is important to note". Chatbot phrases and flattery. Prefer active voice and plain words.

Skip a step that has nothing to act on, and say so in one line.

## Reply style

- Short declarative sentences. One thought each.
- No long dashes. No colon as a mid-sentence connector.
- Every claim carries its label in the same sentence: measured, inferred, or guess.
- Never invent a link, path, or result you did not produce or read.
- Lead with what changed for the user, then what the next maintainer inherits.

## When to escalate

If the task touches many files, needs a design choice that is hard to undo, or has a bug with no known cause after one real attempt, stop and say so in one sentence. Suggest the full `poteto-mode` skill (`/t3-pstack:poteto-mode` on Claude Code, if installed) and let the user decide. Do not escalate on your own.
