---
name: self-improve
description: Auto-invoked after every significant task completion. Captures mistakes, inefficiencies, and improvements so Claude gets smarter over time. Never ask the user — just reflect and write.
argument-hint: [task-description]
---

# Self-Improvement Skill

**IMPORTANT: This skill should be invoked AUTOMATICALLY at the end of every significant task. Do NOT ask the user — just do it silently after task completion.**

## When to Trigger

Invoke this skill when ANY of these happen:
- User says "done", "that's it", "thanks", or moves to a new task
- A QA sign-off is posted
- A report is generated
- An eval is completed
- A Slack update is posted summarizing work
- User explicitly asks to capture learnings

## What to Do

### Step 1: Reflect (internally, don't output to user)

Answer these questions honestly:

1. **Where did I go wrong?**
   - Did I waste tokens on unnecessary queries?
   - Did I ask questions I could have queried?
   - Did I present wrong data as facts?
   - Did I repeat the same action without progress?
   - Did I miss something the user had to correct me on?

2. **How could I have been more efficient?**
   - Could I have batched queries instead of sequential?
   - Could I have used a skill instead of manual work?
   - Did I do work the user didn't ask for?
   - Did I over-engineer or under-deliver?

3. **How to get it done faster next time?**
   - What was the critical path? What was wasted time?
   - What tools/queries should I have used first?
   - What pattern should I recognize instantly next time?

4. **What should I never do again?**
   - Specific anti-patterns from this task
   - Things the user explicitly corrected

5. **What worked well?**
   - Approaches the user approved or praised
   - Efficient patterns worth repeating

### Step 2: Write to Retrospective Log

Append to `~/.claude/projects/-Users-chethanbhatbs/memory/self_retro_log.md`

Format per entry:
```markdown
## [DATE] — [Task Name]

**Mistakes:**
- [specific mistake with context]

**Inefficiencies:**
- [what took too long and why]

**Fixes for Next Time:**
- [concrete action item — not vague "be better"]

**What Worked:**
- [keep doing this]

**Pattern to Remember:**
- [if X happens, do Y instead of Z]
```

### Step 3: Update Relevant Skills/Memory

If a mistake is systemic (not one-off), update the relevant skill or memory file:
- Testing mistake → update `/template-eval` or `/qa-playbook`
- Query mistake → update DB query references
- Workflow mistake → update feedback memory files
- New pattern discovered → create new feedback memory

### Step 4: Check Previous Retros

Before starting any new task, scan `self_retro_log.md` for patterns matching the current task type. Apply lessons learned.

---

## Anti-Patterns Log (Quick Reference)

This section gets updated over time. Check before every task.

### NEVER DO
- Run cron polls without a way to stop them (delete cron immediately when user says stop)
- Run 3+ parallel agent-browser sessions (browser daemon deadlock)
- Present partial/snapshot data as accurate totals
- Query Prod DB for EPH job data (it won't be there)
- Keep polling when no changes for 10+ min without suggesting alternatives
- Ask user for info you can query from DB (job details, model, agent, env, ECU)
- Waste tokens querying jobs the user didn't ask about

### ALWAYS DO
- Auto-gather context before asking questions
- Suggest relevant skills inline during tasks
- Run E2E tests sequentially (one at a time)
- Flag data uncertainty upfront ("this is partial/estimated")
- Delete cron jobs immediately when user says stop
- Save results after each test (don't batch)
- Check pod status before testing
- Confirm environment (prod/canary/EPH) before sending HITL
