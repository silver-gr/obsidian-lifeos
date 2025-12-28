# Obsidian LifeOS

A comprehensive **Integrated Life Management Architecture (ILMA)** for [Obsidian](https://obsidian.md). This system combines the PARA method, periodic notes, habit tracking, goal management, and task workflows into a unified Life Operating System.

![Obsidian](https://img.shields.io/badge/Obsidian-7C3AED?style=flat&logo=obsidian&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green.svg)

## Features

- **PARA Organization** - Projects, Areas, Resources, Archives structure
- **Periodic Notes** - Daily, Weekly, Monthly, Quarterly, Yearly reviews
- **Habit Tracking** - Interactive toggles with Meta Bind, visual charts with Tracker
- **Goal Management** - OKR framework with progress bars and Dataview queries
- **Task Management** - Obsidian Tasks integration with priority sorting
- **Dashboards** - Home, Task, Goal, and Habit dashboards with live data
- **Templater-Powered** - Dynamic templates with automatic date handling

## Quick Start

### 1. Download & Install

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/obsidian-lifeos.git

# Or download as ZIP and extract to your Obsidian vault
```

Copy the `LifeOS/` folder into your existing Obsidian vault, or use this as a new vault.

### 2. Install Required Plugins

Open Obsidian Settings → Community Plugins → Browse, and install:

| Plugin | Purpose | Required |
|--------|---------|----------|
| **Dataview** | Dashboard queries and data aggregation | Yes |
| **Templater** | Dynamic templates with date math | Yes |
| **Tasks** | Task management with priorities and recurrence | Yes |
| **Calendar** | Visual calendar and weekly note creation | Yes |
| **Meta Bind** | Interactive habit toggles and inputs | Recommended |
| **Tracker** | Habit charts and trend visualization | Recommended |
| **Heatmap Calendar** | Yearly habit heatmaps | Optional |

### 3. Configure Plugins

#### Core Daily Notes
Settings → Core Plugins → Daily Notes:
- **Date format:** `YYYY-MM-DD`
- **New file location:** `LifeOS/05-Daily`
- **Template file:** `LifeOS/13-Templates/Daily Note`

#### Templater
Settings → Templater:
- **Template folder:** `LifeOS/13-Templates`
- **Enable "Trigger Templater on new file creation"**
- **Enable "Folder Templates"** and add:

| Folder | Template |
|--------|----------|
| `LifeOS/05-Daily` | `LifeOS/13-Templates/Daily Note.md` |
| `LifeOS/06-Weekly` | `LifeOS/13-Templates/Weekly Review.md` |
| `LifeOS/07-Monthly` | `LifeOS/13-Templates/Monthly Review.md` |
| `LifeOS/01-Projects` | `LifeOS/13-Templates/Project.md` |

#### Calendar (for Weekly Notes)
Settings → Calendar:
- **Show Week Number:** Enable
- **Week Start:** Monday
- **Weekly note format:** `YYYY-[W]ww`
- **Weekly note folder:** `LifeOS/06-Weekly`
- **Weekly note template:** `LifeOS/13-Templates/Weekly Review.md`

### 4. Enable CSS Snippets

Settings → Appearance → CSS Snippets:
- Enable `dashboard-columns.css`

### 5. Start Using

1. Open `LifeOS/12-MOCs/_Home Dashboard.md` as your command center
2. Create your first daily note: `Ctrl/Cmd + P` → "Open today's daily note"
3. Fill in your Vision and Values in `LifeOS/10-Goals/`

## Folder Structure

```
LifeOS/
├── 00-Inbox/           # Quick capture zone
├── 01-Projects/        # Active projects with deadlines
├── 02-Areas/           # Ongoing responsibilities
│   ├── Health/
│   ├── Finance/
│   ├── Career/
│   ├── Learning/
│   └── Relationships/
├── 03-Resources/       # Reference materials
├── 04-Archives/        # Completed/inactive items
├── 05-Daily/           # Daily notes (YYYY-MM-DD.md)
├── 06-Weekly/          # Weekly reviews (YYYY-Www.md)
├── 07-Monthly/         # Monthly reviews (YYYY-MM.md)
├── 08-Quarterly/       # Quarterly reviews (YYYY-Qn.md)
├── 09-Yearly/          # Yearly reviews (YYYY.md)
├── 10-Goals/           # Goal hierarchy
│   ├── Vision.md
│   ├── Values.md
│   └── 2025/Q1-Q4/
├── 11-Habits/          # Habit definitions
├── 12-MOCs/            # Dashboards (Maps of Content)
│   ├── _Home Dashboard.md
│   ├── Task Management MOC.md
│   ├── Goal Tracking MOC.md
│   └── Habit Dashboard MOC.md
└── 13-Templates/       # All templates
```

## Templates Included

| Template | Purpose |
|----------|---------|
| **Daily Note** | Daily journaling, habit tracking, task capture |
| **Weekly Review** | Automated habit rollups, task audit, planning |
| **Monthly Review** | Monthly metrics, goal progress, reflection |
| **Quarterly Review** | OKR review, goal setting, strategic planning |
| **Yearly Review** | Annual reflection and planning |
| **Project** | Project tracking with tasks and progress |
| **Goal** | OKR-style goals with key results |
| **Habit** | Habit definition with implementation intentions |

## Daily Workflow

**Morning (5 min):**
1. Open Home Dashboard
2. Review today's tasks
3. Set top 3 priorities

**Throughout Day:**
1. Log tasks in Daily Note
2. Mark completed items
3. Quick journaling in Log section

**Evening (10 min):**
1. Toggle habit checkboxes
2. Update mood/energy/sleep metrics
3. Reflect on wins and learnings

**Weekly (30-60 min):**
1. Open Weekly Review (click week number in Calendar)
2. Review automated habit summary
3. Audit overdue tasks
4. Plan next week

## Customization

### Adding New Habits

1. Edit `LifeOS/13-Templates/Daily Note.md`
2. Add new property in frontmatter: `new_habit: false`
3. Add toggle in Habits section: `` `INPUT[toggle:new_habit]` New Habit ``
4. Update dashboard queries to include new habit

### Adding New Areas

1. Create folder in `LifeOS/02-Areas/YourArea/`
2. Add to Task Management MOC queries if needed

### Custom Metrics

Add new frontmatter properties to Daily Note template:
```yaml
custom_metric: 0
```

Query in dashboards:
```dataview
TABLE custom_metric FROM "LifeOS/05-Daily" LIMIT 7
```

## Documentation

See [docs/Integrated Life Management Architecture in Obsidian.md](docs/Integrated%20Life%20Management%20Architecture%20in%20Obsidian.md) for the complete theoretical framework and implementation guide.

## Requirements

- Obsidian v1.0.0+
- Required plugins: Dataview, Templater, Tasks, Calendar
- Recommended plugins: Meta Bind, Tracker, Heatmap Calendar

## License

MIT License - Feel free to use, modify, and share.

## Contributing

Contributions welcome! Please open an issue or PR.

## Credits

Built with inspiration from:
- [PARA Method](https://fortelabs.com/blog/para/) by Tiago Forte
- [Obsidian](https://obsidian.md) community
- [Dataview](https://github.com/blacksmithgu/obsidian-dataview) plugin
- [Templater](https://github.com/SilentVoid13/Templater) plugin

---

**Start building your Life Operating System today.**
