# Law Zero: Self-Evolving Claude Code

> **Your Claude Code forgets what it learned yesterday. Law Zero makes it remember — and get smarter every time.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)

---

## The Problem

You spend hours teaching Claude Code your project's rules, tools, and workflows. Then you upgrade a script, add a new skill, or change a config — and suddenly:

- Old instructions conflict with new ones
- Deprecated methods keep getting recommended
- The same mistake happens again because the lesson was lost
- Your `CLAUDE.md` says one thing, your `SKILL.md` says another

**Claude Code has no built-in mechanism to keep itself consistent after changes.**

## The Solution: Law Zero

Law Zero is a **self-evolution framework** for Claude Code. It's a single rule that sits above all other rules — a "zeroth law" that ensures your AI assistant automatically maintains consistency across your entire configuration.

When anything gets upgraded, Law Zero triggers a 4-step protocol:

```
Upgrade → Delete Old → Scan for Conflicts → Verify & Report
```

That's it. No complex setup. No external tools. Just drop it into your `CLAUDE.md` and your Claude Code becomes self-maintaining.

---

## How It Works

### The 4-Step Self-Evolution Protocol

**Step 1 — Implement the Upgrade**
- Deploy the new version, modify the code, update the config

**Step 2 — Delete the Old (Upgrade = Delete)**
- Completely remove all replaced content: code, configs, docs, comments, examples, lesson entries
- Never allow old and new to coexist
- Clean up across ALL files: `CLAUDE.md`, memory files, skill docs, lesson databases

**Step 3 — Global Consistency Scan (Automatic!)**
- Scan all related documents and configs for contradictions, conflicts, and outdated references
- Scope covers your entire Claude Code configuration:
  - `CLAUDE.md` — Main project instructions
  - Memory files (`*.md`) — Persistent memory
  - Lesson files (`*.json`) — Learned patterns
  - Skill files (`SKILL.md`) — Skill documentation
  - Workspace files — Any shared agent configs
- Found a contradiction? **Fix it immediately**, no need to ask the user
- Found an outdated reference? **Delete or update it immediately**

**Step 4 — Verify & Report**
- Confirm all files are consistent, no contradictions remain
- Report what was upgraded, what was deleted, what conflicts were resolved

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

**Rules:**
1. **Before any operation** — Check lessons for known pitfalls
2. **After any mistake** — Write the lesson to a file immediately
3. **Categories auto-expand** — No predefined limits, create new files as needed

Each lesson is a simple JSON entry:
```json
{
  "date": "2026-02-18",
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

With Law Zero:
```
Day 1: Teach Claude Code to use Tool A
Day 5: Upgrade to Tool B → Law Zero auto-triggers:
       ✓ Deletes all Tool A references
       ✓ Scans every file for "Tool A" mentions
       ✓ Updates examples, lessons, and configs
       ✓ Reports: "Upgraded Tool A → B, cleaned 4 files, fixed 2 conflicts"
Day 6: Claude Code consistently uses Tool B everywhere
```

---

## Quick Start

### 1. Copy the Law Zero block into your `CLAUDE.md`

Add this at the **very top** of your `CLAUDE.md`, before any other rules:

```markdown
## Law Zero: Self-Evolution Mechanism (Highest Priority!)

**This is the zeroth law of the system. Any upgrade operation must execute this mechanism first.**

### Trigger
When ANY feature, skill, script, project, document, or config is upgraded or updated,
**immediately execute the following 4-step protocol:**

### Protocol (4 steps, all required)

**Step 1 — Implement the Upgrade**
- Complete the new version deployment/modification/replacement

**Step 2 — Delete the Old (Upgrade = Delete)**
- Completely remove all replaced content: code, configs, docs, comments, examples, lesson entries
- Never allow old and new versions to coexist
- Clean up across ALL files that reference the upgraded component

**Step 3 — Global Consistency Scan (Automatic!)**
- Scan all related documents and configs for contradictions with the new version
- Scan scope:
  - `CLAUDE.md` — Main instructions
  - Memory files — Persistent memory
  - Lesson files — Learned patterns
  - Skill docs — Skill documentation
  - Workspace files — Shared configs
- Found contradiction → Fix immediately, no need to ask
- Found outdated reference → Delete or update immediately

**Step 4 — Verify & Report**
- Confirm all files are consistent
- Report: what changed, what was deleted, what conflicts were resolved

### Core Principles
- This is a self-learning mechanism: every upgrade makes the system cleaner
- Proactively eliminate contradictions: don't wait for the user to find problems
- Only keep the latest and best: all components always at their newest version
```

### 2. (Optional) Set up the Lesson Learning System

Create a lessons directory:
```bash
mkdir -p ~/.claude/lessons
```

Add this to your `CLAUDE.md`:
```markdown
## Lesson Learning System

### Lesson Database
Location: `~/.claude/lessons/*.json`
Each JSON file = one category. File name = category name.

### Rules
1. **Before any operation** — Check relevant lesson files for known pitfalls
2. **After any mistake** — Write the lesson to a file immediately
3. **Categories auto-expand** — Need a new category? Create a new JSON file

### JSON Format (all categories use this)
{
  "category": "Category Name",
  "lessons": [
    {
      "date": "YYYY-MM-DD",
      "rule": "One-line rule",
      "detail": "Full explanation with commands and reasoning."
    }
  ]
}
```

### 3. Done!

That's it. No packages to install, no dependencies, no build step. Law Zero works purely through Claude Code's instruction-following capability.

---

## Full Template

For a complete, production-ready `CLAUDE.md` template with Law Zero and the Lesson Learning System pre-configured, see:

**[`templates/CLAUDE.md`](templates/CLAUDE.md)**

---

## Real-World Example

This framework was born from running Claude Code as a remote assistant on macOS, controlled via Feishu (Lark) messaging. Over weeks of daily use, we discovered:

- **15 conflicting instructions** across 8 configuration files
- Skills documentation recommending **deprecated methods** that had been replaced
- Lesson files teaching one thing while `CLAUDE.md` taught the opposite
- New upgrades silently breaking old workflows because docs weren't updated

After implementing Law Zero, every upgrade now triggers an automatic scan. The system caught and fixed all 15 conflicts in a single pass. No more "wait, why is it doing that?" moments.

## Design Philosophy

**1. Convention over Configuration**
- No external tools needed. Law Zero works through natural language instructions.
- Claude Code already follows `CLAUDE.md` — we just give it a meta-rule about maintaining `CLAUDE.md` itself.

**2. Single Source of Truth**
- Each piece of knowledge lives in exactly one place.
- Other files point to the source, they don't duplicate it.
- When the source changes, pointers still work. Duplicates would become stale.

**3. Fail-Safe by Default**
- If Law Zero can't determine whether something is outdated, it flags it rather than silently removing it.
- Verification step ensures no accidental data loss.
- The report step creates an audit trail of all changes.

**4. Progressive Enhancement**
- Start with just the Law Zero block in `CLAUDE.md` (30 seconds to set up)
- Add the Lesson Learning System when you want persistent knowledge
- Add custom scan paths as your project grows
- The framework scales from solo projects to complex multi-agent setups

---

## FAQ

**Q: Does this work with Claude Code only?**
A: Law Zero is designed for Claude Code (Anthropic's CLI), but the concept applies to any LLM-powered coding assistant that reads instruction files. The principle — "when you upgrade, scan for conflicts" — is universal.

**Q: Will this slow down my workflow?**
A: The scan happens only when something is upgraded, not on every interaction. For most upgrades, the scan takes seconds. The time saved from not debugging stale instructions far outweighs it.

**Q: What if Claude Code makes a mistake during the scan?**
A: Step 4 (Verify & Report) creates visibility. Claude Code reports exactly what it changed, so you can review. If something was incorrectly modified, you can revert it.

**Q: Can I customize the scan paths?**
A: Absolutely. The scan scope in Step 3 is just a list of paths. Add or remove paths based on your project structure.

**Q: How is this different from just writing good documentation?**
A: Good documentation tells Claude Code what to do. Law Zero tells it how to maintain that documentation as things change. It's meta-documentation — rules about rules.

---

## Contributing

Found a way to improve Law Zero? PRs are welcome!

- Add new template configurations for different use cases
- Share your custom lesson categories
- Improve the scan heuristics
- Translate the templates

---

## License

MIT License. Use it, modify it, share it.

---

## Star This Repo

If Law Zero saved you from debugging stale instructions, give it a star. It helps other Claude Code users find it.

---

*Built with real pain and real solutions from daily Claude Code usage. Every rule in Law Zero exists because we hit the problem it solves.*
