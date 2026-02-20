# Example: Law Zero v3 in Action

## Scenario 1: The Bug That Inspired v2.0 (Cross-Project Contamination)

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

These changes were correct for XHS, but `CLAUDE.md` is shared by ALL projects. The Page Agent section now had warnings that weren't relevant to WeChat.

**Next day**: WeChat `send-file` went to the wrong person — global config changes shifted system behavior.

### What Happens with v2.0+ (Project Mode)

Same upgrade, but Law Zero defaults to Project Mode:

```
Step 3 — Project-scoped scan (XHS project only):
  Modified: skills/xiaohongshu-ops/SKILL.md  — Updated v2→v3
  Modified: scripts/xhs-auto-reply.js         — Rewritten to native CDP
  NOT modified: CLAUDE.md                      — Read-only in project mode ✓
  NOT modified: MEMORY.md                      — Read-only in project mode ✓
```

**Result**: XHS upgraded, WeChat untouched. No cross-contamination.

---

## Scenario 2: The Bug That Inspired v3.0 (No Rollback)

### Background
You upgrade a critical bridge script from v7 to v8, adding multi-bot support.

### What Happened with v2.0 (Immediate Delete)

```
Step 2 — Delete old:
  Deleted: bridge.sh v7 (permanently removed)
  Created: bridge.sh v8 (new multi-bot version)

Day 2: v8 has a race condition — lock file conflict causes message drops
Day 3: Can't rollback. v7 is gone. Must debug v8 live under production pressure.
```

Another case:
```
Step 2 — Delete old:
  Deleted: chrome-auto.sh old --user-data-dir approach
  Created: chrome-auto.sh new Default profile approach

Day 2: Chrome 145 security restriction blocks new approach entirely
Day 3: Must reconstruct old approach from memory. 2 hours wasted.
```

### What Happens with v3.0 (Safe Upgrade)

```
Step 2 — Deprecate old:
  Moved: bridge.sh v7 → .deprecated/2026-02-20/bridge.sh
  Created: bridge.sh v8

Step 4 — Observation period starts (24-48h)

Day 2: v8 has a race condition
  → cp .deprecated/2026-02-20/bridge.sh ./bridge.sh  (10-second rollback!)
  → Fix v8 calmly, re-deploy

Day 4: v8 fixed and stable for 48h

Step 5 — Clean deprecated:
  Deleted: .deprecated/2026-02-20/bridge.sh
```

**Result**: Zero downtime. Zero panic. The old version was right there when needed.

---

## Scenario 3: WeChat Safety Fix (Project Mode + Safe Upgrade)

Upgrading WeChat automation from v3.4 to v3.5 (safety fix for wrong-recipient bug):

```
Step 2 — Deprecate old:
  Moved: wechat-ax.py v3.4 → .deprecated/2026-02-20/wechat-ax.py
  Deployed: wechat-ax.py v3.5

Step 3 — Project-scoped consistency scan finds 8 issues:
  Fixed: SKILL.md missing v3.5 safety feature (navigate failure → abort send)
  Fixed: SKILL.md missing v3.4 pinyin matching docs
  Fixed: SKILL.md missing "known issues" table
  Fixed: lessons/wechat.json "4-level nav" → "5-level nav"
  Added: lessons/wechat.json — "send must check navigate return value"
  Added: lessons/wechat.json — "WeChat 0-window recovery with open -a"

Step 4 — Report + observation:
  Files modified (3): SKILL.md, lessons/wechat.json, wechat-ax.py
  Files NOT modified: CLAUDE.md, MEMORY.md (read-only in project mode)
  Observation: 48h of successful message sends

Step 5 — Clean deprecated:
  Deleted: .deprecated/2026-02-20/wechat-ax.py
  All WeChat project files now consistent at v3.5
```

---

## Scenario 4: When to Use Global Mode

You're reorganizing your entire tool stack — replacing Playwright with a new browser automation framework across ALL projects.

```
User: "Run global Law Zero — replacing Playwright with BrowserX everywhere"

Step 2 — Deprecate old:
  Moved: Multiple Playwright-related files → ~/.deprecated/2026-02-20/

Step 3 — Global scan:
  Modified: CLAUDE.md           — Tool priority table updated
  Modified: MEMORY.md           — All project descriptions updated
  Modified: lessons/web.json    — Playwright lessons archived, BrowserX lessons added
  Modified: skills/page-agent/SKILL.md    — Rewritten for BrowserX
  Modified: skills/xiaohongshu-ops/SKILL.md — Updated automation references

Step 4 — Observation period (48h recommended for global changes)

Step 5 — Clean ~/.deprecated/2026-02-20/ after stable observation
```

Global Mode is appropriate here because the change genuinely affects every project.

---

## Scenario 5: Skipping Observation (Trivial Changes)

User: "Update the typo in SKILL.md, skip observation, delete now"

```
Step 2 — Deprecate: moved old SKILL.md to .deprecated/ (still do this!)
Step 3 — Scan: no contradictions found
Step 4 — Report: listed the change. User said "skip observation"
Step 5 — Clean: immediately deleted .deprecated/
```

For trivial changes, the user can explicitly skip the observation period.

---

## Key Takeaways

1. **Default to Project Mode** — It's safer. Most upgrades only affect one project.
2. **Use Global Mode intentionally** — Only for changes that truly affect everything.
3. **Deprecate, don't delete** — `.deprecated/` is cheap insurance against irreversible mistakes.
4. **Observation period is passive** — You keep working while the new version proves itself.
5. **The file list in Step 4 is mandatory** — You always know exactly what changed.
6. **Rollback is fast** — One `cp` command from `.deprecated/` vs. hours of reconstruction.
7. **User can skip observation** — For trivial changes, just say "skip observation, delete now".
