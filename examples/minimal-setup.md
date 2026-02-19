# Minimal Setup (30 Seconds)

The simplest way to use Law Zero v2 — just add this block to the **top** of your existing `CLAUDE.md`:

```markdown
## Law Zero: Self-Evolution (Highest Priority!)

Two modes — Project Mode is the default:
- **Project Mode**: "Run Law Zero on [project]" → only modify project files, global files read-only
- **Global Mode**: "Run global Law Zero" → can modify everything

When anything is upgraded, execute this 4-step protocol:

1. **Upgrade** — Deploy the change
2. **Delete Old** — Remove ALL replaced content (within scope only!)
3. **Scan** — Check scoped files for contradictions, fix them immediately
4. **Report** — List every file modified, confirm consistency

Project Mode: scan project SKILL.md, scripts/*, data/*. Read (don't write) CLAUDE.md, memory, lessons.
Global Mode: scan and modify everything.
Never allow old and new to coexist. Fix contradictions within scope.
```

That's it. 12 lines. Your Claude Code now self-maintains **without accidentally breaking other projects**.

## What Changed from v1?

v1's minimal setup had no scope concept — every scan could modify any file. v2 defaults to project-scoped, which is safer for multi-project setups.

## Want More?

- Add the [Lesson Learning System](../templates/CLAUDE.md#lesson-learning-system) for persistent knowledge
- Add [custom scan paths](../templates/CLAUDE.md#step-3--consistency-scan) for your project structure
- See the [full template](../templates/CLAUDE.md) for a production-ready configuration
