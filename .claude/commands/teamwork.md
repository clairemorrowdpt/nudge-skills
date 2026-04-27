---
description: Update the shared Teamwork page with this week's and last week's tasks for the PT Consultants team, then remind you to push to GitHub Pages
---

Update the shared teamwork page at `docs/team.html` in this repo. This file is what gets deployed to GitHub Pages for the whole team to view.

Today's date is available in your context (`currentDate`). "This week" = Mon–Sun of the current week. "Last week" = the prior Mon–Sun.

**This skill is for the page manager (Claire). Teammates view the page at the GitHub Pages URL — they don't run this skill.**

---

## Commercial Clinical Consultants

Pull from **Asana project GID: 1200768211331439** (PT Commercial, Marketing, CS).

| Name | Asana GID |
|---|---|
| Bijal Toprani | 1198711097297533 |
| Christynne Helfrich | 1201500391989257 |
| Jillian Kleiner | 1206284657569481 |

For each person:
1. Use `mcp__asana__asana_get_tasks` or `mcp__asana__asana_search_tasks` to fetch their tasks from the project
2. Tasks **due this week** → This Week section (active, not done style)
3. Tasks **completed or due last week** → Last Week section (done style, strikethrough)
4. Count the Last Week tasks and update `<span class="count-pill">N done</span>`

---

## Product Clinical Consultants

The Product team cards contain manually-maintained pod update summaries. **Do not overwrite these** unless specifically asked. The "This Week" and "Last Week" cells show "Asana data source coming soon" — leave as-is unless you have new data to add.

---

## HTML format for task items

**This Week (active):**
```html
<div class="task-item">
  <div class="task-dot"></div>
  <div>
    <a href="https://app.asana.com/1/32993968966741/project/1200768211331439/task/TASK_GID" target="_blank">Task Name — Contact</a>
    <span class="badge monitor">Apr 28</span>
  </div>
</div>
```

**Last Week (done):**
```html
<div class="task-item task-done">
  <div class="task-dot"></div>
  <div>
    <a href="https://app.asana.com/1/32993968966741/project/1200768211331439/task/TASK_GID" target="_blank">Task Name — Contact</a>
  </div>
</div>
```

Badge types: `badge monitor` (blue, for dates) · `badge inperson` (orange, for in-person events)

For tasks without a known GID, link to the project:
`href="https://app.asana.com/1/32993968966741/project/1200768211331439"`

---

## What to replace in the file

For each commercial consultant card, replace only:
- The `<div class="task-list">` block inside the **This Week** card-section
- The `<div class="task-list" id="[name]-last">` block inside the **Last Week** card-section
- The count pill text: `<span class="count-pill">N done</span>`

Leave everything else (CSS, JS, product team cards, nav, header) untouched.

---

## After updating

Remind the user to commit and push so GitHub Pages updates:

```bash
cd ~/nudge-skills
git add docs/team.html
git commit -m "teamwork: update week of [Monday date]"
git push
```

GitHub Pages redeploys automatically within ~60 seconds of the push.
