# Example: Law Zero v2 in Action

## Scenario 1: The Bug That Inspired v2.0

### Background
You have two projects sharing the same tool (Page Agent):
- **XHS (Xiaohongshu) auto-reply** — Uses Page Agent via CDP for notification scraping
- **WeChat automation** — Uses Page Agent via Accessibility API for message sending

### What Happened with v1.0 (Global Mode Only)

Running Law Zero on the XHS project after upgrading from Playwright to raw CDP:

```
Step 3 — Global scan found contradictions:
  Modified: CLAUDE.md      — Updated Page Agent section with CDP limitations
  Modified: lessons/web.json — Added Playwright CDP incompatibility lesson
  Modified: MEMORY.md      — Updated XHS description to v3
```

These changes were correct for XHS, but `CLAUDE.md` is shared by ALL projects. The Page Agent section now had warnings that weren't relevant to WeChat (which uses Accessibility API, not CDP).

**Next day**: WeChat `send-file` to "File Transfer Assistant" went to the wrong person. Investigation showed the navigation code was fine — but the broader system behavior had shifted due to global config changes.

### What Happens with v2.0 (Project Mode)

Same upgrade, but now Law Zero defaults to Project Mode:

```
Step 3 — Project-scoped scan (XHS project only):
  Modified: skills/xiaohongshu-ops/SKILL.md  — Updated v2→v3, architecture section
  Modified: scripts/xhs-auto-reply.js         — Rewritten to native CDP
  Modified: scripts/xhs-autoreply-cron.sh      — Added auto-start, network check
  NOT modified: CLAUDE.md                      — Read-only in project mode ✓
  NOT modified: MEMORY.md                      — Read-only in project mode ✓
  NOT modified: lessons/web.json               — Read-only in project mode ✓
```

**Result**: XHS project fully upgraded. WeChat project completely untouched. No cross-contamination.

---

## Scenario 2: WeChat Safety Fix (Project Mode)

Upgrading WeChat automation from v3.4 to v3.5 (safety fix for wrong-recipient bug):

**Project Mode scan** finds 8 issues within WeChat project files:

```
Step 2 — Delete old:
  Updated: SKILL.md header v3.1.1 → v3.5
  Updated: SKILL.md "send" description — removed "AXValue priority" (outdated since v3.2)

Step 3 — Consistency scan (project files only):
  Fixed: SKILL.md missing v3.5 safety feature (navigate failure → abort send)
  Fixed: SKILL.md missing v3.4 pinyin matching docs
  Fixed: SKILL.md missing "known issues" table
  Fixed: lessons/wechat.json "4-level nav" → "5-level nav" (v3.4 added level 5)
  Added: lessons/wechat.json — "send must check navigate return value"
  Added: lessons/wechat.json — "WeChat 0-window recovery with open -a"

Step 4 — Report:
  Files modified (3): SKILL.md, lessons/wechat.json, wechat-ax.py
  Files NOT modified: CLAUDE.md, MEMORY.md (read-only in project mode)
  All WeChat project files now consistent at v3.5
```

---

## Scenario 3: When to Use Global Mode

You're reorganizing your entire tool stack — replacing Playwright with a new browser automation framework across ALL projects.

```
User: "Run global Law Zero — replacing Playwright with BrowserX everywhere"

Step 3 — Global scan:
  Modified: CLAUDE.md           — Tool priority table updated
  Modified: MEMORY.md           — All project descriptions updated
  Modified: lessons/web.json    — Playwright lessons archived, BrowserX lessons added
  Modified: skills/page-agent/SKILL.md    — Rewritten for BrowserX
  Modified: skills/xiaohongshu-ops/SKILL.md — Updated automation references
  Modified: skills/wechat/SKILL.md         — Updated (if applicable)
```

Global Mode is appropriate here because the change genuinely affects every project.

---

## Key Takeaways

1. **Default to Project Mode** — It's safer. Most upgrades only affect one project.
2. **Use Global Mode intentionally** — Only for changes that truly affect everything.
3. **The file list in Step 4 is mandatory** — You always know exactly what changed.
4. **Read-only doesn't mean ignore** — Project Mode reads global files to check for contradictions, but fixes them in project files instead of modifying global configs.
