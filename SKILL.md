---
name: poteto-lite
description: Cheap, in-chat version of poteto-mode. Use only when the user types /poteto-lite or asks for lite poteto. Runs understand, design, build, prove and cleanup in this chat. No subagents, no review panel, no big skill reads.
---

# Poteto lite

Work in this chat only. Start no subagents, no `delegate_task`, no panel review, and do not read `t3-pstack:poteto-mode` or its playbooks. Say so in one line if a step would normally have delegated.

## Habits

- **Data first.** Name the data shape before writing logic.
- **Smallest change.** Delete before you add. No new abstraction for one caller.
- **Bug means root cause.** Reproduce it first, trace the symptom to its cause, fix it once where all callers route through.
- **Prove it.** Run the real artifact (test, CLI, app, page) and report what you ran. "It compiles" is not proof.
- **Don't block on the human.** On reversible work, pick a sensible default, do it, and say what you chose. Ask only for irreversible or product calls.
- **Candor over agreement.** If the request or approach does not earn its place, say so.
- **No comments** unless the code cannot show a non-obvious why.

## Flow

Run these in order, in this chat. Skip a phase with nothing to act on and say so in one line.

1. **Understand.** Read only the files the task touches. Restate the goal in one sentence. A question about code or a read-only investigation ends here with an answer.
2. **Design.** Name the data shape and the interface. For anything non-trivial, write two approaches in a few lines each, pick one, and give the reason. Stop and ask only if the choice is hard to undo. For UI work, read one installed design skill (`frontend-design`, `apple-design` or `web-design-guidelines`). Otherwise read none.
3. **Build.**
   - Bug: write the failing test or repro first, then fix the root cause.
   - Feature: build from the named data shape, smallest working slice first.
   - Refactor: keep behavior identical and lean on existing tests.
   - Make small edits and keep the diff reviewable.
4. **Prove.** Run the real thing and report the command and the result. If you cannot run it, say so and label the claim a guess.
5. **Cleanup.** Run the three steps below.
6. **Reply.** Follow the reply style below.

## Cleanup before you finish

1. **Code changed.** Run the `deslop` skill on the diff if your harness has one (`t3-pstack:deslop` on Claude Code). Otherwise apply its rules yourself. Remove comments that are unnecessary or off the local style. Remove defensive checks and try/catch that are abnormal for trusted code paths. Remove `any` casts used only to dodge type errors. Flatten deep nesting with early returns. Keep behavior unchanged and edits small.
2. **Comments.** Read the diff for comments and delete each one that is not a non-obvious why the code cannot show. Do not spawn comment-sicko. For the full subagent version, the user types `/t3-pstack:no-comments`.
3. **Prose written.** Run the `unslop` skill (`t3-pstack:unslop` on Claude Code) on any doc, README, PR description, or commit message you wrote, and on your final reply when it runs longer than a few sentences. Without that skill, cut these yourself. AI vocabulary such as "additionally", "crucial", "delve", "pivotal" and "showcase". "Serves as" and "boasts" where "is" or "has" works. "Not just X, but Y". Em dashes, and colons used as mid-sentence connectors. Bold lead-ins that restate the line. Filler like "in order to" and "it is important to note". Chatbot phrases and flattery. Prefer active voice and plain words.

## Reply style

- Short declarative sentences. One thought each.
- No long dashes. No colon as a mid-sentence connector.
- Every claim carries its label in the same sentence: measured, inferred, or guess.
- Never invent a link, path, or result you did not produce or read.
- Lead with what changed for the user, then what the next maintainer inherits.

## When to escalate

If the task touches many files, needs a design choice that is hard to undo, or has a bug with no known cause after one real attempt, stop and say so in one sentence. Suggest the full `poteto-mode` skill (`/t3-pstack:poteto-mode` on Claude Code, if installed) and let the user decide. Do not escalate on your own.
