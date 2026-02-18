# Example: Law Zero in Action

## Scenario: Upgrading a WeChat Automation Script

You have a WeChat automation script that used AppleScript + screencapture for sending messages. You've just rewritten it to use the macOS Accessibility API instead.

### Without Law Zero

You update the script and move on. But:

- Your `CLAUDE.md` still has the old AppleScript template (130 lines of outdated code)
- Your `SKILL.md` still says "use screencapture to verify messages"
- Your `lessons/wechat.json` still has a lesson about "Chinese text must use clipboard with AppleScript keystroke"
- Your `memory/wechat-automation.md` still references the old script name
- A teammate's `workspace/TOOLS.md` still lists the old command

**Result**: Claude Code randomly uses the old method 40% of the time, causing failures. You spend hours debugging "why does it keep using the old script?"

### With Law Zero

After updating the script, Law Zero automatically triggers:

**Step 1** — The new Accessibility API script is deployed. Done.

**Step 2** — Delete old:
```
Deleted: CLAUDE.md lines 200-330 (old AppleScript WeChat template)
Deleted: lessons/wechat.json entry about "AppleScript keystroke for Chinese"
Updated: SKILL.md "verification" section (removed screencapture, added API JSON check)
```

**Step 3** — Global scan found 3 more issues:
```
Fixed: memory/wechat-automation.md — still referenced old script name
Fixed: workspace/TOOLS.md — still listed old command
Fixed: lessons/general.json — had "use screencapture to verify" (conflicts with new API approach)
```

**Step 4** — Report:
```
Upgrade complete: WeChat automation AppleScript → Accessibility API
- Deleted: 130 lines of old templates from CLAUDE.md
- Updated: 3 lesson entries
- Fixed: 3 contradictions across memory and workspace files
- All 8 scanned files now consistent
```

**Result**: Claude Code uses the new API method 100% of the time. Zero confusion.

---

## Scenario: Adding a New Tool to Your Workflow

You've just discovered that Page Agent (CDP + semantic operations) is better than raw Playwright for logged-in page interactions.

### Law Zero Protocol

**Step 1** — Add Page Agent documentation to your `CLAUDE.md`

**Step 2** — Update the tool priority table:
```diff
- | Page interaction | Playwright | Click buttons, fill forms |
+ | Page interaction (public) | Playwright headless | Search, data extraction |
+ | Page interaction (logged-in) | Page Agent (CDP) | Click buttons, fill forms |
```

**Step 3** — Scan finds:
```
Conflict: lessons/web.json says "use Playwright connectOverCDP for logged-in pages"
  → Updated to: "use Page Agent for logged-in pages, Playwright for public sites"

Conflict: memory/operational-lessons.md has Playwright CDP code example
  → Deleted (Page Agent replaces this use case)

Outdated: SKILL.md still says "Playwright is the only browser automation tool"
  → Updated to include Page Agent
```

**Step 4** — Everything consistent.

---

## Key Takeaway

Law Zero doesn't just update one file — it updates the **entire knowledge graph** of your Claude Code configuration. This is what makes it fundamentally different from just "writing good documentation."
