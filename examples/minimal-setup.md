# Minimal Setup (30 Seconds)

The simplest way to use Law Zero v3 — just add this block to the **top** of your existing `CLAUDE.md`:

```markdown
## Law Zero: Self-Evolution (Highest Priority!)

Two modes — Project Mode is the default:
- **Project Mode**: "Run Law Zero on [project]" → only modify project files, global files read-only
- **Global Mode**: "Run global Law Zero" → can modify everything

When anything is upgraded, execute this 5-step protocol:

1. **Upgrade** — Deploy the change
2. **Deprecate Old** — Move replaced files to `.deprecated/YYYY-MM-DD/` (DON'T delete!)
3. **Scan** — Check scoped files for contradictions, fix them immediately
4. **Observe** — List every file modified, run new version 24-48h in production
5. **Clean** — After observation, delete `.deprecated/` files

Project Mode: scan project SKILL.md, scripts/*, data/*. Read (don't write) CLAUDE.md, memory, lessons.
Global Mode: scan and modify everything.
Old files go to .deprecated/ — your safety net until the new version proves itself.
```

That's it. 14 lines. Your Claude Code now self-maintains **with rollback safety**.

## What Changed from v2?

v2's Step 2 was "Delete Old (Upgrade = Delete)" — immediate, irreversible removal. v3 replaces this with "Deprecate Old" — files are moved to `.deprecated/` and only cleaned up after 24-48 hours of stable production use. This gives you a rollback path when the new version has issues.

## What Changed from v1?

v1 had no scope concept — every scan could modify any file. v2 added project-scoped scanning. v3 adds safe upgrades with rollback.

## Want More?

- Add the [Lesson Learning System](../templates/CLAUDE.md#lesson-learning-system) for persistent knowledge
- Add [custom scan paths](../templates/CLAUDE.md#step-3--consistency-scan) for your project structure
- See the [full template](../templates/CLAUDE.md) for a production-ready configuration
