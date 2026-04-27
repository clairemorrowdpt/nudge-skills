# nudge-skills

Claude Code skill suite for the PT Consultants team at Hinge Health.

- **Teamwork** — shared weekly overview of team engagements, hosted on GitHub Pages
- **Nudge** — personal daily action-item dashboard, generated locally per person

---

## For the team: set up your personal Nudge page

### Prerequisites
- [Claude Code](https://claude.ai/code) installed
- Glean, Gmail, and Asana MCP servers connected in Claude Code

### One-time setup

```bash
# 1. Clone this repo
git clone <repo-url> ~/nudge-skills

# 2. Install the skill commands globally
mkdir -p ~/.claude/commands
cp ~/nudge-skills/.claude/commands/* ~/.claude/commands/

# 3. Create your config
mkdir -p ~/nudge
cp ~/nudge-skills/nudge-config.example.md ~/nudge/nudge-config.md
# Open ~/nudge/nudge-config.md and fill in your name, email, role, Asana GID, and the Teamwork URL
```

### Using your nudge page

In Claude Code, run:
```
/nudge
```

Claude will search your email, calendar, docs, Slack, and Asana, then generate (or update) `~/nudge/index.html`. Open that file in any browser.

Run `/nudge` any morning to refresh it. **Your page is private** — it lives only on your machine.

### Customizing your sources

Edit `~/nudge/nudge-config.md` and tell Claude what to change next time you run `/nudge`. For example:
- "Skip Gmail, I manage that separately"
- "Add Jira — my project key is XYZ"
- "Add a section called 'RFP Queue' for clinical SME requests"

---

## For the page manager: updating Teamwork

The Teamwork page (`docs/team.html`) is updated by the team manager and deployed to GitHub Pages.

### Update workflow

```bash
# Make sure you're in the repo
cd ~/nudge-skills

# In Claude Code, run:
/teamwork
# Claude pulls Asana data and updates docs/team.html

# Review the changes, then commit and push
git add docs/team.html
git commit -m "teamwork: update week of <Monday date>"
git push
```

GitHub Pages redeploys automatically within ~60 seconds.

---

## GitHub Pages setup (one-time, done by repo owner)

1. Create a new GitHub repo (e.g. `nudge-skills`)
2. Push this directory to it:
   ```bash
   cd ~/nudge-skills
   git init
   git add .
   git commit -m "initial commit"
   git remote add origin https://github.com/<your-username>/nudge-skills.git
   git push -u origin main
   ```
3. In the GitHub repo settings → **Pages** → set source to **Deploy from a branch**, branch `main`, folder `/docs`
4. Your Teamwork page will be live at:
   `https://clairemorrowdpt.github.io/nudge-skills/team.html`
5. Share that URL with your team and add it to your `nudge-config.md` as the Teamwork URL

---

## File structure

```
nudge-skills/
├── .claude/
│   └── commands/
│       ├── nudge.md       ← /nudge skill (personal dashboard)
│       └── teamwork.md    ← /teamwork skill (manager only)
├── docs/                  ← GitHub Pages source
│   ├── index.html         ← Landing page with setup instructions
│   └── team.html          ← Shared Teamwork page
├── templates/
│   └── nudge-template.html ← Base template for new nudge pages
├── nudge-config.example.md ← Copy to ~/nudge/nudge-config.md
└── README.md
```
