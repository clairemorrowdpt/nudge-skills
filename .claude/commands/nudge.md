---
description: Update my personal nudge dashboard with current action items from email, calendar, Slack, and Asana
---

Update my personal nudge page at `~/nudge/index.html` for today.

Today's date is available in your context (`currentDate`). Use it throughout — for removing stale items, dating new ones, and labeling the Asana This Week section header.

## Step 1 — Read my config

Check if `~/nudge/nudge-config.md` exists and read it. The config specifies:
- Who I am (name, email, role)
- Which data sources to use or skip
- My Asana project GID(s), if applicable
- Any focus areas or custom notes
- The shared Teamwork page URL (for the nav link)

If the config doesn't exist, proceed with all default sources and offer to generate a starter config at the end based on what you learned about me.

## Step 2 — Read my current nudge page

Read `~/nudge/index.html`. If it doesn't exist, read `~/nudge-skills/templates/nudge-template.html` and write it to `~/nudge/index.html` first, then work from there.

Note all existing items (by data-id and topic) so you don't re-add anything already present.

## Step 3 — Gather fresh data

Search each configured source. Cast a wide net — better to surface an extra item than to miss something.

### Glean (docs, Slack, company knowledge)
Use `mcp__glean_default__search` with queries like:
- `[my name] action needed`
- `[my name] please review`
- `[my name] assigned` (meeting notes, trackers)
- `from:[my manager's name] updated:past_week`
- Recent docs from close collaborators where I have open comments or assigned items

### Gmail
Use `mcp__glean_default__gmail_search` for emails in the last 2 weeks where:
- I'm asked to respond, approve, or take action
- A colleague is following up with me
- A deadline is mentioned and I need to act

### Google Calendar
Use `mcp__glean_default__meeting_lookup` for my meetings today and this week. Look for:
- Meetings I'm presenting at or leading → Action Required with date badge
- Prep calls ahead of important meetings → Action Required with date badge
- Key upcoming events worth monitoring → Monitor

### Asana
Use `mcp__asana__asana_search_tasks` or `mcp__asana__asana_get_tasks`. If my config specifies a project GID, search that project. Otherwise search tasks assigned to me across all workspaces.
- Tasks due this week → Asana This Week section
- Tasks due in the next 4 weeks or recently assigned → Asana Upcoming / Recently Assigned section

## Step 4 — Update the page

### Remove stale items
Remove items with a specific past date that is more than 1 day ago. Keep:
- Undated items (no specific due date)
- Monitor items without a date
- Items with future dates

### Update recurring items
If a recurring meeting is listed with a past date (e.g., a weekly standup), update its badge date to the next occurrence rather than removing it.

### Add new items
Place each new item in the correct section:

| What it is | Section |
|---|---|
| Email/doc response needed, approval, deadline-driven task | Action Required |
| Meeting I'm presenting or leading | Action Required (with date badge) |
| Prep call before a meeting | Action Required (with date badge) |
| Watch item, no immediate action needed | Monitor / No Immediate Action |
| Unanswered Slack DM or @mention | Slack — Needs Reply |
| Asana task due this week | Asana — This Week |
| Asana task due later / recently assigned | Asana — Upcoming / Recently Assigned |

Update the **Asana This Week section heading** (`<h2>`) to show the current week's Mon–Sun date range, e.g. `Asana — This Week (Apr 27–May 3)`.

**Do not add duplicates.** If an item covering the same topic is already in the page, skip it.

## Item HTML format

```html
<div class="item" data-id="unique-kebab-id" onclick="toggle(this)">
  <div class="checkbox">
    <svg width="11" height="8" viewBox="0 0 11 8" fill="none">
      <path d="M1 4L4 7L10 1" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </div>
  <div class="content">
    <div class="item-title"><a href="URL" target="_blank" onclick="event.stopPropagation()">Title</a> <span class="badge TYPE">Label</span></div>
    <div class="item-desc">What needs to be done and any relevant context.</div>
    <div class="item-meta">From Person / Source · Date</div>
  </div>
</div>
```

**Badge types:**
- `badge urgent` — red; due today, overdue, or needs immediate response
- `badge monitor` — blue; upcoming date or watch item
- `badge slack` — purple; Slack DM or @mention
- `badge inperson` — orange; in-person event or travel

**data-id:** Short, unique kebab-case. Examples: `q2-rfp-review`, `asana-tw-may6-keurig`, `slack-dm-from-jane`.

## Known bug
To reveal the Resolved section use `resolvedSection().style.display = 'block'` — **not** `display = ''`, which falls back to the CSS `display:none` rule.

## Teamwork page nav link
If the user's config includes a `Teamwork URL`, make sure the nav `<a href="...">Teamwork</a>` link at the top of the page points to that URL. If no URL is configured, leave it pointing to `team.html` (local fallback).
