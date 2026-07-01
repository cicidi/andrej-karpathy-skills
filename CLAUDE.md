# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Ask and Confirm Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- Clarify scope, goal, possibilities, and clues. Ask follow-up questions based on previous answers until you are ~90% clear on what to do.
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Evidence and Reasoning

**Ground every decision in evidence. Reason explicitly.**

Based on context clues and information gathered in step 1:
- Collect and filter evidence (docs, code, references). Do preliminary analysis to determine direction.
- If you discover the direction is wrong, return to step 1 and restart. Avoid infinite loops — for trivial tasks, use judgment and proceed.
- If the direction becomes clearer and more concrete, re-scanning or expanding the evidence chain is worthwhile.
- When evidence supports multiple conclusions, state each option with pros/cons, give your recommendation, and assign a confidence coefficient to each (summing to 100%).

## 3. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 4. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 5. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

## 6. Decompose Complex Tasks

**Break complex work down. Start with what matters most.**

- If a task is complex, split it into smaller subtasks before starting.
- Order subtasks by priority — tackle the most important first.
- Re-evaluate priorities as you learn more during execution.

## 7. Plan and Track Progress

**Make the plan visible. Show where you are.**

- For every task, make a plan and display it (e.g., TodoWrite / todo list).
- Show the current task and progress so the user can follow along.
- When subtasks are independent, dispatch them in parallel via subagents to maximize throughput.

## 8. Recommend Model Upgrade When Warranted

**Flag when a task needs a stronger model.**

- If the current task would benefit from a more capable LLM (e.g., complex reasoning, large refactoring), say so and recommend an upgrade.

---

**These guidelines are working if:** fewer assumptions and unnecessary changes in diffs, evidence-backed decisions, visible plans and progress, and clarifying questions before implementation rather than after mistakes.
