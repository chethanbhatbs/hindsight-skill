# Self-Improve — Claude Code Skill

Auto-invoked after every significant task completion. Captures mistakes, inefficiencies, and improvements so Claude gets smarter over time.

## Usage

```
/self-improve [task-description]
```

Runs automatically — never asks the user. Reflects on the completed task and records:
- What went wrong (mistakes, wasted steps)
- What went right (efficient patterns, good decisions)
- What to do differently next time
- Updates the retro log at `~/.claude/projects/*/memory/self_retro_log.md`

## How it works

1. Reviews the conversation for mistakes and inefficiencies
2. Identifies patterns to avoid or repeat
3. Writes findings to the retro log
4. Future conversations read the retro log to avoid repeating mistakes

## Installation

```bash
cp -r self-improve ~/.claude/skills/
```

## License

MIT
