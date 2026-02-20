# Law Zero: Self-Evolving Claude Code

> **Your Claude Code forgets what it learned yesterday. Law Zero makes it remember — and get smarter every time.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)
[![Version](https://img.shields.io/badge/Version-3.0-brightgreen)](https://github.com/shi557636shi/claude-code-law-zero)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/shi557636shi/claude-code-law-zero/pulls)

---

## What's New in v3.0

**Safe Upgrades with Rollback** (the biggest change!) — Law Zero no longer deletes old versions immediately. Instead, deprecated files are moved to `.deprecated/` with a date stamp, giving you a 24-48 hour observation period to catch issues before permanent cleanup. This prevents the #1 cause of cascading failures: deleting the old version before the new one is battle-tested.

| Feature | v1.0 | v2.0 | v3.0 |
|---------|------|------|------|
| Consistency scan | Always global | Project-scoped default | Project-scoped default |
| Global files | Modified freely | Read-only in project mode | Read-only in project mode |
| Cross-project safety | Not addressed | Projects isolated | Projects isolated |
| Old version handling | Delete immediately | Delete immediately | **Deprecate → Observe → Clean** |
| Rollback capability | None | None | **Quick rollback from .deprecated/** |
| Protocol steps | 4 steps | 4 steps | **5 steps** |

---

## The Problem

You spend hours teaching Claude Code your project's rules, tools, and workflows. Then you upgrade a script, add a new skill, or change a config — and suddenly:

- Old instructions conflict with new ones
- Deprecated methods keep getting recommended
- The same mistake happens again because the lesson was lost
- Your `CLAUDE.md` says one thing, your `SKILL.md` says another
- **Worse: fixing Project A's docs accidentally breaks Project B** (v2.0 solved this!)
- **Even worse: the old version was deleted, the new version has a bug, and there's no way back** (v3.0 solves this!)

**Claude Code has no built-in mechanism to keep itself consistent after changes.**

## The Solution: Law Zero

Law Zero is a **self-evolution framework** for Claude Code. It's a single rule that sits above all other rules — a "zeroth law" that ensures your AI assistant automatically maintains consistency across your configuration.

When anything gets upgraded, Law Zero triggers a 5-step protocol:

```
Upgrade → Deprecate Old → Scan for Conflicts → Observe → Clean Up
```

No complex setup. No external tools. Just drop it into your `CLAUDE.md` and your Claude Code becomes self-maintaining.

---

## How It Works

### Two Scan Modes (since v2.0)

This is the most important concept in Law Zero. Getting the scope right prevents cascading bugs across projects.

| Mode | When to Use | Scan Scope | Global Files |
|------|------------|------------|-------------|
| **Project Mode** (default) | "Run Law Zero on Project X" | Only files in that project directory | **Read-only** (never modified) |
| **Global Mode** | "Run a global Law Zero scan" | All projects + global files | Read and write |

**Why Project Mode is the default:**
- Project A and Project B might share the same tool (e.g., Playwright) but use it differently
- Modifying global files during Project A's scan could break Project B
- Over multiple rounds, global files get modified back and forth — increasing entropy
- **Each project's Law Zero optimizes only itself, never touching other projects**

**When to use Global Mode:**
- Major infrastructure changes affecting all projects
- Periodic full-system consistency checks
- When you explicitly want to update global configs

### The 5-Step Safe Evolution Protocol (v3.0)

**Step 1 — Implement the Upgrade**
- Deploy the new version, modify the code, update the config

**Step 2 — Deprecate the Old (Don't Delete!)**
- Move replaced files to a `.deprecated/` directory (within scope), **not** delete them
  - **Project Mode**: `project-directory/.deprecated/YYYY-MM-DD/`
  - **Global Mode**: `~/.deprecated/YYYY-MM-DD/`
- Preserve directory structure inside `.deprecated/` for easy rollback
- Mark deprecated items in docs/code: "Deprecated — replaced by XX"
- **Why not delete immediately?** The new version hasn't been battle-tested yet. The old version is your only safety net.

**Step 3 — Consistency Scan**
- **Project Mode** scans (only modifies project files):
  - Project's `SKILL.md`
  - Project's `scripts/*`, `data/*`, `config/*`
  - Reads (but does NOT write) global files to check for contradictions
  - If project files contradict global files → fix the project files, not global
- **Global Mode** scans (can modify all files):
  - `CLAUDE.md` — Main project instructions
  - Memory files — Persistent memory
  - Lesson files — Learned patterns
  - All `SKILL.md` files — Skill documentation
  - Workspace files — Shared configs
- Found a contradiction? **Fix it within scope**, never cross boundaries

**Step 4 — Verify & Observation Period**
- Confirm all files within scope are consistent, no contradictions remain
- **List every modified file** — full transparency
- Report: what was upgraded, what was deprecated, what conflicts were resolved
- **Observation period**: New version must run in production for 24-48 hours
  - During observation: if the new version has issues → quick rollback from `.deprecated/`
  - During observation: do NOT clean up `.deprecated/`

**Step 5 — Clean Deprecated Files (After Observation)**
- After 24-48 hours of stable production use, confirm no other scripts/projects still reference the old version
- Only then permanently delete the `.deprecated/` files
- If the user explicitly says "skip observation, delete now" → you may skip the observation period

### Why v3.0? The Real-World Pain

v2.0 solved cross-project contamination, but we kept hitting another problem:

```
Day 1: Upgrade bridge.sh v7 → v8, delete v7 immediately
Day 2: v8 has an edge-case bug (lock file race condition)
Day 3: Can't rollback — v7 is gone. Must debug v8 live under pressure.
```

```
Day 1: Upgrade Chrome automation to use Default profile, delete old --user-data-dir approach
Day 2: Chrome 145 security restriction blocks the new approach entirely
Day 3: Must reconstruct the old approach from memory — wastes 2 hours.
```

With v3.0:
```
Day 1: Upgrade bridge.sh v7 → v8, move v7 to .deprecated/2026-02-20/
Day 2: v8 has a bug → copy v7 back from .deprecated/ in 10 seconds
Day 3: Fix v8 calmly, re-deploy, observe again
Day 4: v8 stable → delete .deprecated/
```

### The Lesson Learning System

Law Zero includes a dynamic lesson learning system that captures and persists knowledge:

```
~/.claude/lessons/
  ├── general.json      # General principles
  ├── web.json          # Web automation lessons
  ├── wechat.json       # Domain-specific lessons
  ├── git.json          # Git operation lessons
  └── <any-topic>.json  # Auto-created as needed
```

**Three Iron Rules:**
1. **Before any operation** — Check lessons for known pitfalls
2. **After any mistake** — Write the lesson to a file immediately ("saying you'll remember doesn't count — write it to a file")
3. **Categories auto-expand** — No predefined limits, create new files as needed

Each lesson is a simple JSON entry:
```json
{
  "date": "2026-02-19",
  "rule": "One-line rule (what to do / what not to do)",
  "detail": "Full explanation with commands, reasoning, and correct approach."
}
```

### Why It Matters

Without Law Zero:
```
Day 1: Teach Claude Code to use Tool A
Day 5: Upgrade to Tool B, forget to update CLAUDE.md
Day 6: Claude Code uses Tool A (old docs) and Tool B (new memory) randomly
Day 7: You waste 30 minutes debugging why it's using the wrong tool
```

With Law Zero v1 (Global Mode only):
```
Day 5: Upgrade to Tool B → Law Zero triggers:
       ✓ Deletes all Tool A references everywhere
       ✗ Accidentally modifies shared config used by Project C
Day 8: Project C breaks
```

With Law Zero v2 (Project Mode):
```
Day 5: Upgrade Project B to use Tool B → Project Mode:
       ✓ Deletes Tool A references in Project B only
       ✓ Project C untouched
       ✗ Tool B has a bug — Tool A is already gone, no rollback
```

With Law Zero v3 (Safe Upgrade):
```
Day 5: Upgrade Project B to use Tool B → Project Mode:
       ✓ Tool A moved to .deprecated/ (not deleted)
       ✓ Project C untouched
Day 6: Tool B has a bug → restore Tool A from .deprecated/ in seconds
Day 8: Tool B fixed and stable → clean .deprecated/
```

---

## Quick Start

### 1. Copy the Law Zero block into your `CLAUDE.md`

Add this at the **very top** of your `CLAUDE.md`, before any other rules:

```markdown
## Law Zero: Self-Evolution Mechanism (Highest Priority!)

**This is the zeroth law. Any upgrade must execute this mechanism first.**

### Scope Rules (Most Important!)

Two modes — Project Mode is the default:

| Mode | Trigger | Scope | Global Files |
|------|---------|-------|-------------|
| **Project Mode** (default) | "Run Law Zero on [project]" | Only project files | Read-only |
| **Global Mode** | "Run global Law Zero" | All files | Read + Write |

**Project Mode rule**: Global files (CLAUDE.md, memory, lessons) are READ-ONLY.
Fix contradictions by changing project files, not global files.

### Protocol (5 Steps, All Required)

**Step 1 — Upgrade**: Deploy the change
**Step 2 — Deprecate Old**: Move replaced files to `.deprecated/YYYY-MM-DD/` (DON'T delete!)
**Step 3 — Consistency Scan**: Check all files in scope for contradictions, fix immediately
**Step 4 — Verify & Observe**: List every file modified, observe 24-48h in production
**Step 5 — Clean Up**: After observation period, delete `.deprecated/` files
```

### 2. (Optional) Set up the Lesson Learning System

```bash
mkdir -p ~/.claude/lessons
```

Add the Lesson Learning System rules to your `CLAUDE.md` (see [`templates/CLAUDE.md`](templates/CLAUDE.md) for the full template).

### 3. Done!

No packages to install, no dependencies, no build step. Law Zero works purely through Claude Code's instruction-following capability.

---

## Full Template

For a complete, production-ready `CLAUDE.md` template with Law Zero v3 and the Lesson Learning System pre-configured:

**[`templates/CLAUDE.md`](templates/CLAUDE.md)**

---

## Real-World Examples

### The Bug That Inspired v2.0 (Cross-Project Contamination)

We ran Law Zero on a Xiaohongshu (XHS) auto-reply project. The scan found contradictions and "fixed" them by modifying global files — which broke the WeChat automation project that shared Page Agent. v2.0 introduced Project Mode to prevent this.

### The Bug That Inspired v3.0 (No Rollback)

We upgraded `bridge.sh` from v7 to v8 and immediately deleted v7. When v8 had a race condition bug, we couldn't roll back. We also tried to consolidate Chrome profiles — deleted the old `--user-data-dir` approach, only to discover Chrome 145 blocks CDP on default profiles. Had to reconstruct the old approach from memory. v3.0 introduces the deprecation pattern so you always have a safety net.

See [`examples/`](examples/) for detailed scenarios.

---

## Design Philosophy

**1. Project Isolation (v2.0)**
- Each project's Law Zero optimizes only itself
- Global files are shared infrastructure — treat them with care
- Cross-project contamination is the #1 source of cascading bugs

**2. Safe Upgrades (v3.0)**
- Deprecate before delete — always keep a rollback path
- Observation period catches bugs before they become permanent
- `.deprecated/` is cheap insurance against irreversible mistakes

**3. Convention over Configuration**
- No external tools needed. Works through natural language instructions.
- Claude Code already follows `CLAUDE.md` — we give it a meta-rule about maintaining itself.

**4. Single Source of Truth**
- Each piece of knowledge lives in exactly one place.
- When the source changes, pointers still work. Duplicates become stale.

**5. Fail-Safe by Default**
- Verification step ensures no accidental data loss.
- The report step creates an audit trail of all changes.
- **File modification list is mandatory** — you always know what was changed.

**6. Progressive Enhancement**
- Start with just the Law Zero block (30 seconds to set up)
- Add the Lesson Learning System for persistent knowledge
- Add custom scan paths as your project grows
- Scales from solo projects to complex multi-agent setups

---

## Version History

| Version | Date | Key Change |
|---------|------|-----------|
| v1.0 | 2026-02-18 | Initial release — 4-step protocol with global scanning |
| v2.0 | 2026-02-19 | Project-scoped scanning — prevent cross-project contamination |
| v3.0 | 2026-02-20 | Safe upgrades — deprecate→observe→clean instead of immediate delete |

---

## FAQ

**Q: What changed in v3.0?**
A: Step 2 changed from "Delete Old" to "Deprecate Old" — files are moved to `.deprecated/` instead of being deleted. A new Step 5 handles cleanup after a 24-48 hour observation period. This gives you rollback capability when the new version has issues.

**Q: What changed in v2.0?**
A: The default scan mode became project-scoped instead of global. Global files (CLAUDE.md, memory, lessons) are read-only in project mode. This prevents one project's cleanup from breaking another.

**Q: Does this work with Claude Code only?**
A: Designed for Claude Code (Anthropic's CLI), but the concept applies to any LLM coding assistant that reads instruction files. The principle — "when you upgrade, deprecate the old, scan for conflicts within the right scope, and observe before cleaning up" — is universal.

**Q: Will this slow down my workflow?**
A: The scan happens only when something is upgraded. The observation period runs passively — you keep working while the new version proves itself. Time saved from not debugging irreversible mistakes far outweighs it.

**Q: Can I skip the observation period?**
A: Yes — tell Claude "skip observation, delete now" and it will clean up `.deprecated/` immediately. Useful for trivial changes where rollback isn't needed.

**Q: What if `.deprecated/` gets too big?**
A: Clean it periodically. Each entry is date-stamped, so you can easily identify old entries. A simple `rm -rf .deprecated/2026-01-*` clears everything from January.

**Q: Should I ever use Global Mode?**
A: Yes — for periodic full-system checks, major infrastructure changes, or when you explicitly want to update global configs. Just be intentional about it.

---

## Contributing

Found a way to improve Law Zero? PRs are welcome!

- Share your project-scoped scan configurations
- Add new template configurations for different use cases
- Share your custom lesson categories
- Improve the scan heuristics
- Translate the templates

---

## License

MIT License. Use it, modify it, share it.

---

## Star This Repo

If Law Zero saved you from debugging stale instructions, cross-project contamination, or irreversible deletions, give it a star. It helps other Claude Code users find it.

---

*Built with real pain and real solutions from daily Claude Code usage. v3.0 was born from deleting a working script before its replacement was proven — and spending hours reconstructing it from memory. Never again.*
