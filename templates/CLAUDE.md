# Project Instructions

<!--
  LAW ZERO v3.0 TEMPLATE — Drop this into your project's CLAUDE.md
  Key changes from v2: Safe upgrades with .deprecated/ rollback.
  Customize the sections below for your specific project.
-->

---

## Law Zero: Self-Evolution Mechanism (Highest Priority! Above All Rules!)

**This is the zeroth law of the system. Any upgrade operation must execute this mechanism first.**

### Scope Rules (Most Important!)

**Law Zero has two modes. Project Mode is the default:**

| Mode | Trigger | Scan/Modify Scope | Global Files |
|------|---------|-------------------|-------------|
| **Project Mode** (default) | "Run Law Zero on [project]" | Only files in the project directory | **Read-only** |
| **Global Mode** | "Run global Law Zero" | All projects + global files | Read + Write |

**Project Mode rules:**
- Only scan and modify files within the target project (SKILL.md, scripts/*, data/*, config/*)
- Global files (CLAUDE.md, memory, lessons) are **read-only** — read them to check for contradictions, but fix project files, not global ones
- Different projects may share the same tools but use them differently — never let one project's scan affect another

**Why not always modify global files:**
- Project A and B might share Playwright, Page Agent, etc., but with different usage patterns
- Modifying global files during Project A's scan → might break Project B
- Over multiple rounds → global files get modified back and forth → increasing entropy

### Trigger Condition
When ANY feature, skill, script, project, document, or configuration is upgraded or updated,
**immediately and automatically execute the following complete protocol:**

### Execution Protocol (5 Steps — All Required)

**Step 1 — Implement the Upgrade**
- Complete the new version's deployment, modification, or replacement

**Step 2 — Deprecate the Old (Don't Delete!)**
- Move replaced files to `.deprecated/` directory (within scope), **NOT** delete them
  - **Project Mode**: `project-directory/.deprecated/YYYY-MM-DD/`
  - **Global Mode**: `~/.deprecated/YYYY-MM-DD/`
- Preserve directory structure inside `.deprecated/` for easy rollback
- Mark deprecated items in docs/code: "Deprecated — replaced by XX"
- **Why**: The new version hasn't been battle-tested. The old version is your safety net.

**Step 3 — Consistency Scan**
- **Project Mode** scan scope (only modifies project files):
  - Project's `SKILL.md`
  - Project's `scripts/*`, `data/*`, `config/*`
  - Reads (but does NOT write) global files to check for contradictions
  - If project files contradict global → fix project files, not global
- **Global Mode** scan scope (can modify all files):
  - `CLAUDE.md` — Main project instructions
  - Memory files — Persistent memory
  - Lesson files — Learned patterns
  - All `SKILL.md` files — Skill documentation
  - Workspace files — Shared configs
- Found a contradiction → **Fix it within scope**, never cross boundaries
- Found an outdated reference → **Update within scope**

**Step 4 — Verify & Observation Period**
- Confirm all files within scope are consistent, no contradictions remain
- **List every modified file** — full transparency for the user
- Report:
  - What was upgraded
  - What old content was deprecated (moved to `.deprecated/`)
  - What contradictions were found and resolved
  - Confirmation that all scoped files are now consistent
- **Observation period**: New version must run in production for 24-48 hours
  - During observation: if the new version has issues → quick rollback from `.deprecated/`
  - During observation: do NOT clean up `.deprecated/`

**Step 5 — Clean Deprecated Files (After Observation)**
- After 24-48 hours of stable production use
- Confirm no other scripts/projects still reference the old version
- Only then permanently delete the `.deprecated/` files
- If user explicitly says "skip observation, delete now" → may skip observation period

### Core Principles
- **Project isolation**: Each project's Law Zero optimizes only itself, never affecting other projects
- **Global files are sacred**: Only modify when user explicitly requests Global Mode
- **Safe upgrades**: Deprecate → Observe → Clean. Never make irreversible changes prematurely
- **Quick rollback**: `.deprecated/` is your safety net during the observation period
- **Transparent changes**: Every report must include a complete file modification list

---

## Lesson Learning System

### Overview
A dynamic, file-based knowledge system that captures lessons learned and prevents repeated mistakes.

### Lesson Database Location
```
.claude/lessons/*.json    <- Each JSON file is one category
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
- Operation failed or produced unexpected results -> Record cause and correct approach
- Discovered a more efficient method -> Record comparison (old vs. new)
- User corrected a mistake -> Record the user's correct approach
- Solved a tricky problem -> Record the diagnostic process and solution

### Pre-Operation Lesson Check Flow
1. Determine the type of operation about to be executed
2. Read the corresponding lesson file (e.g., git operation -> `git.json`)
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
- After [operation type] -> [verification method]
- After [operation type] -> [verification method]
