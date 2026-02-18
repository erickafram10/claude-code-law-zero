# Project Instructions

<!--
  LAW ZERO TEMPLATE — Drop this into your project's CLAUDE.md
  Customize the sections below for your specific project.
  The Self-Evolution Mechanism (Law Zero) stays at the top, always.
-->

---

## Law Zero: Self-Evolution Mechanism (Highest Priority! Above All Rules!)

**This is the zeroth law of the system. Any upgrade operation must execute this mechanism first.**

### Trigger Condition
When ANY feature, skill, script, project, document, or configuration is upgraded or updated,
**immediately and automatically execute the following complete protocol:**

### Execution Protocol (4 Steps — All Required)

**Step 1 — Implement the Upgrade**
- Complete the new version's deployment, modification, or replacement

**Step 2 — Delete the Old (Upgrade = Delete)**
- **Completely remove** all replaced old-version content, including:
  - Code and scripts
  - Configuration files and entries
  - Documentation descriptions, comments, and examples
  - Lesson database entries that reference the old version
- Absolutely no coexistence of old and new versions
- Clean up across ALL related files

**Step 3 — Global Consistency Scan (Automatic!)**
- Scan **all related documents and configurations** for content that contradicts, conflicts with, or is outdated by the new version
- Default scan scope (customize for your project):
  - `CLAUDE.md` — Main project instructions
  - `memory/*.md` — Persistent memory files (if using auto-memory)
  - `lessons/*.json` — Lesson database files
  - `skills/*/SKILL.md` — Skill documentation
  - Any other instruction files your project uses
- Found a contradiction → **Fix it immediately**, no need to ask the user
- Found an outdated reference → **Delete or update it immediately**

**Step 4 — Verify & Report**
- Confirm all files are consistent, no contradictions remain
- Report to the user:
  - What was upgraded
  - What old content was deleted
  - What contradictions were found and resolved
  - Confirmation that all files are now consistent

### Core Principles
- **Self-learning mechanism**: Every upgrade makes the entire system cleaner and more consistent
- **Proactive contradiction elimination**: Don't wait for the user to discover problems — find and fix them during upgrade
- **Only the latest and best**: All project components, skills, and tools always stay at their newest version
- **Instruction files updated first**: Any upgrade is immediately reflected in CLAUDE.md and related instruction files

---

## Lesson Learning System

### Overview
A dynamic, file-based knowledge system that captures lessons learned and prevents repeated mistakes.

### Lesson Database Location
```
.claude/lessons/*.json    ← Each JSON file is one category
```

### Three Iron Rules

**Rule 1 — Check lessons before any operation**
Before executing any significant operation, scan relevant lesson files for known pitfalls.
Matching is by category (file name) and keyword search across `rule` fields.

**Rule 2 — Write lessons after any mistake**
Every unexpected result, discovered pitfall, or better method must be written to a lesson file **immediately**.
"Saying you'll remember is not enough — write it to a file."

**Rule 3 — Categories auto-expand**
No predefined category limits. When a lesson doesn't fit any existing file, create a new JSON file.
File name = category name. No registration needed.

### Lesson File Format (Universal)
```json
{
  "category": "Human-readable category name",
  "lessons": [
    {
      "date": "YYYY-MM-DD",
      "rule": "One-line rule (what to do / what NOT to do)",
      "detail": "Full explanation including: root cause, correct approach, specific commands/code, and why the old way was wrong."
    }
  ]
}
```

### When to Write a Lesson
- Operation failed or produced unexpected results → Record cause and correct approach
- Discovered a more efficient method → Record comparison (old vs. new)
- User corrected a mistake → Record the user's correct approach
- Solved a tricky problem → Record the diagnostic process and solution

### Pre-Operation Lesson Check Flow
1. Determine the type of operation about to be executed
2. Read the corresponding lesson file (e.g., git operation → `git.json`)
3. If unsure which category, search all files' `rule` fields by keyword
4. Adjust the execution plan based on lessons found

---

## Project-Specific Rules

<!-- Add your project's specific rules below -->

### Core Principles
1. **[Your principle 1]**
2. **[Your principle 2]**
3. **[Your principle 3]**

### Tools & Workflows
<!-- Define your project's tools, their priority, and when to use each -->

| Tool | Use Case | Example |
|------|----------|---------|
| [Tool 1] | [When to use] | [Example] |
| [Tool 2] | [When to use] | [Example] |

### Verification Rules
<!-- Define how to verify operations in your project -->
- After [operation type] → [verification method]
- After [operation type] → [verification method]
