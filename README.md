# Law Zero: Self-Evolving Claude Code

> **Your Claude Code forgets what it learned yesterday. Law Zero makes it remember — and get smarter every time.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)
[![Version](https://img.shields.io/badge/Version-2.0-brightgreen)](https://github.com/shi557636shi/claude-code-law-zero)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/shi557636shi/claude-code-law-zero/pulls)

---

## What's New in v2.0

**Project-Scoped Mode** (the biggest change!) — Law Zero now defaults to scanning only within the target project. Global files are read-only unless you explicitly request a full global scan. This prevents cross-project contamination when multiple projects share common tools.

| Feature | v1.0 | v2.0 |
|---------|------|------|
| Consistency scan | Always global | **Project-scoped by default** |
| Global files (CLAUDE.md, memory) | Modified freely | **Read-only in project mode** |
| Cross-project safety | Not addressed | **Projects isolated from each other** |
| Scan mode selection | One mode only | **Two modes: Project (default) + Global** |

---

## The Problem

You spend hours teaching Claude Code your project's rules, tools, and workflows. Then you upgrade a script, add a new skill, or change a config — and suddenly:

- Old instructions conflict with new ones
- Deprecated methods keep getting recommended
- The same mistake happens again because the lesson was lost
- Your `CLAUDE.md` says one thing, your `SKILL.md` says another
- **Worse: fixing Project A's docs accidentally breaks Project B** (v2.0 solves this!)

**Claude Code has no built-in mechanism to keep itself consistent after changes.**

## The Solution: Law Zero

Law Zero is a **self-evolution framework** for Claude Code. It's a single rule that sits above all other rules — a "zeroth law" that ensures your AI assistant automatically maintains consistency across your configuration.

When anything gets upgraded, Law Zero triggers a 4-step protocol:

```
Upgrade → Delete Old → Scan for Conflicts → Verify & Report
```

No complex setup. No external tools. Just drop it into your `CLAUDE.md` and your Claude Code becomes self-maintaining.

---

## How It Works

### Two Scan Modes (v2.0)

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

### The 4-Step Self-Evolution Protocol

**Step 1 — Implement the Upgrade**
- Deploy the new version, modify the code, update the config

**Step 2 — Delete the Old (Upgrade = Delete)**
- Completely remove all replaced content (within scope)
- Never allow old and new to coexist
- **Project Mode**: Only clean files within the project directory
- **Global Mode**: Clean all files including CLAUDE.md, memory, lessons

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

**Step 4 — Verify & Report**
- Confirm all files within scope are consistent
- **List every modified file** — full transparency
- Report: what changed, what was deleted, what conflicts were resolved

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

With Law Zero (v1 — Global Mode):
```
Day 5: Upgrade to Tool B → Law Zero auto-triggers:
       ✓ Deletes all Tool A references everywhere
       ✓ But also accidentally modifies a shared config used by Project C
Day 8: Project C breaks because its Tool A config was removed
```

With Law Zero v2 (Project Mode):
```
Day 5: Upgrade Project B to use Tool B → Law Zero triggers in Project Mode:
       ✓ Deletes Tool A references in Project B's files only
       ✓ Reads global config (doesn't modify it)
       ✓ Project C's Tool A config is untouched
Day 6: Both projects work perfectly, no cross-contamination
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

### Protocol (4 Steps, All Required)

**Step 1 — Upgrade**: Deploy the change
**Step 2 — Delete Old**: Remove ALL replaced content (within scope only)
**Step 3 — Consistency Scan**: Check all files in scope for contradictions, fix immediately
**Step 4 — Verify & Report**: List every file modified, confirm consistency
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

For a complete, production-ready `CLAUDE.md` template with Law Zero v2 and the Lesson Learning System pre-configured:

**[`templates/CLAUDE.md`](templates/CLAUDE.md)**

---

## Real-World Examples

### The Bug That Inspired v2.0

We ran Law Zero on a Xiaohongshu (XHS) auto-reply project. The scan found contradictions and "fixed" them by modifying:
- `CLAUDE.md` (global) — Updated Page Agent section
- `lessons/web.json` (global) — Added CDP lessons
- `MEMORY.md` (global) — Updated project description

These changes were correct for XHS, but they affected the WeChat automation project too, which shared Page Agent but used it differently. The next WeChat file-send operation went to the wrong person because the global config had been altered.

**Solution**: Law Zero v2 defaults to Project Mode. The XHS scan would only modify XHS's own files (`SKILL.md`, `scripts/*`). Global files become read-only references.

### Typical Upgrade Scenario

Upgrading a WeChat automation script from AppleScript to Accessibility API:

**Project Mode scan** (default):
```
Modified: skills/wechat/SKILL.md  — v3.1 → v3.5, updated all sections
Modified: lessons/wechat.json     — Added 3 new lessons (safety fix, 0-window recovery)
Modified: scripts/wechat-ax.py    — Added navigation safety checks
NOT modified: CLAUDE.md           — Read-only in project mode ✓
NOT modified: MEMORY.md           — Read-only in project mode ✓
```

See [`examples/`](examples/) for more detailed scenarios.

---

## Design Philosophy

**1. Project Isolation (v2.0)**
- Each project's Law Zero optimizes only itself
- Global files are shared infrastructure — treat them with care
- Cross-project contamination is the #1 source of cascading bugs

**2. Convention over Configuration**
- No external tools needed. Works through natural language instructions.
- Claude Code already follows `CLAUDE.md` — we give it a meta-rule about maintaining itself.

**3. Single Source of Truth**
- Each piece of knowledge lives in exactly one place.
- When the source changes, pointers still work. Duplicates become stale.

**4. Fail-Safe by Default**
- Verification step ensures no accidental data loss.
- The report step creates an audit trail of all changes.
- **File modification list is mandatory** — you always know what was changed.

**5. Progressive Enhancement**
- Start with just the Law Zero block (30 seconds to set up)
- Add the Lesson Learning System for persistent knowledge
- Add custom scan paths as your project grows
- Scales from solo projects to complex multi-agent setups

---

## FAQ

**Q: What changed in v2.0?**
A: The default scan mode is now project-scoped instead of global. Global files (CLAUDE.md, memory, lessons) are read-only in project mode. You must explicitly request "global Law Zero" to modify shared files. This prevents one project's cleanup from breaking another.

**Q: Does this work with Claude Code only?**
A: Designed for Claude Code (Anthropic's CLI), but the concept applies to any LLM coding assistant that reads instruction files. The principle — "when you upgrade, scan for conflicts within the right scope" — is universal.

**Q: Will this slow down my workflow?**
A: The scan happens only when something is upgraded. Project-scoped scans are even faster since they check fewer files. Time saved from not debugging stale instructions far outweighs it.

**Q: What if Claude Code modifies the wrong file?**
A: v2.0's Project Mode prevents this by design — global files are read-only. The mandatory file list in Step 4 also gives you full visibility.

**Q: Can I customize the scan paths?**
A: Yes. The scan scope is just a list of paths. Customize per project.

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

If Law Zero saved you from debugging stale instructions or cross-project contamination, give it a star. It helps other Claude Code users find it.

---

*Built with real pain and real solutions from daily Claude Code usage. v2.0 was born from a bug that sent a file to the wrong person — because a project-specific scan accidentally modified a shared WeChat config. Never again.*
