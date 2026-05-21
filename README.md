# Self-Improve — Claude Code Skill

Auto-invoked after every significant task. Captures mistakes, inefficiencies, and improvements so Claude gets smarter over time.

## Prerequisites

- [Claude Code](https://claude.ai/claude-code) CLI installed
- GitHub CLI (`gh`) for one-line install

## Installation

**One-line install:**

```bash
gh repo clone chethanbhatbs/hindsight-skill ~/.claude/skills/hindsight
```

**Manual install:**

```bash
git clone https://github.com/chethanbhatbs/hindsight-skill.git
cp -r self-improve-skill/ ~/.claude/skills/hindsight/
```

**Verify it's installed:**

```bash
ls ~/.claude/skills/hindsight/
```

You should see `SKILL.md` (and any other skill files).

## Usage

```
/self-improve [task-description]    # Manually trigger a retro
```

### What it does

Runs automatically after task completion — you don't need to invoke it. It:

1. Reviews the conversation for mistakes and wasted steps
2. Identifies what went right (efficient patterns, good decisions)
3. Records findings in `~/.claude/projects/*/memory/self_retro_log.md`
4. Future conversations read the retro log to avoid repeating mistakes

### Example retro entry

```
## 2026-04-09 — JSON Diff Setup
- MISTAKE: Read entire 2000-line file when only needed lines 45-60
- FIX: Use Grep first to find line numbers, then targeted Read
- GOOD: Batched 3 independent tool calls in parallel
```



## How Claude Code Skills Work

Skills are markdown files in `~/.claude/skills/` that give Claude Code specialized instructions for specific tasks. When you invoke a skill (e.g., `/Self-Improve`), Claude reads the `SKILL.md` and follows its instructions.

## Uninstall

```bash
rm -rf ~/.claude/skills/hindsight
```

---

<p align="center">
  <sub>Built with <a href="https://emergent.sh">Emergent</a> + <a href="https://claude.ai/code">Claude Code</a> · refined by hand</sub>
</p>
