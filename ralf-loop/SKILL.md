---
name: ralf-loop
description: Ralph-style looping workflow for complex tasks using a file-based prompt, status, and acceptance checklist. Use when the user says "ralf-loop" or asks for an iterative loop that continues until acceptance criteria are marked done.
---

# Ralf Loop

## Overview
Run a file-driven loop that re-reads the same prompt and instructions, executes work, updates status, and continues until all acceptance criteria are marked done in green.

## Philosophy
- Iteration > perfection: use the loop to refine work over multiple passes.
- Failures are data: deterministic failures inform how to tune prompts.
- Operator skill matters: strong prompts drive successful loops.
- Persistence wins: keep iterating until success criteria are met.

## When to use
Good for:
- Well-defined tasks with clear success criteria.
- Tasks needing iteration and refinement (for example, getting tests to pass).
- Greenfield tasks where you can walk away between iterations.
- Tasks with automatic verification (tests, linters).

Not good for:
- Tasks requiring human judgment or design decisions.
- One-shot operations.
- Tasks with unclear success criteria.
- Production debugging (prefer targeted debugging).

## Workflow
1) Initialize loop workspace
   - Ensure `ralf-loop/` exists in the repo root.
   - If missing, copy templates from `.agent/skills/ralf-loop/assets/ralf-loop-template/`.
2) Load loop inputs
   - Read `ralf-loop/PROMPT.md` for task statement and completion promise.
   - Read `ralf-loop/INSTRUCTIONS.md` for the latest user-provided implementation guidance.
   - Read `ralf-loop/CHECKLIST.md` for acceptance criteria.
3) Plan and execute
   - Update or create `task_plan.md` with the current plan.
   - Perform the necessary repo changes to satisfy acceptance criteria.
4) Record progress
   - Update `progress.md` with what changed and what remains.
   - Update `ralf-loop/STATUS.md` with a concise iteration summary and blockers.
5) Verify acceptance criteria
   - Run required tests or verification steps automatically.
   - If no explicit test command is provided, choose the most relevant test target and run it.
   - Record test results in `progress.md`.
6) Evaluate completion
   - Mark checklist items as green DONE only after verification passes.
   - If all checklist items are marked done in green, set `LOOP_STATE: DONE` in `ralf-loop/STATUS.md`.
   - Otherwise set `LOOP_STATE: CONTINUE` and wait for the next user loop prompt.

## Checklist conventions
- Store acceptance criteria in `ralf-loop/CHECKLIST.md`.
- Mark an item done as green using HTML, e.g. `<span style="color: green;">DONE</span>`.
- Keep unchecked items clearly labeled as `TODO`.

## Artifacts
- `ralf-loop/PROMPT.md`: fixed task prompt and completion promise.
- `ralf-loop/INSTRUCTIONS.md`: user-provided implementation details (updated between iterations).
- `ralf-loop/CHECKLIST.md`: acceptance criteria, tracked to completion.
- `ralf-loop/STATUS.md`: per-iteration status and loop state.
- `task_plan.md`: current plan for the iteration.
- `progress.md`: running log of progress.

## Notes
- The loop runs across turns; re-read files each iteration.
- Do not change the prompt or acceptance criteria unless the user updates them.
