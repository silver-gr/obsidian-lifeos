---
cssclass: dashboard
tags:
  - dashboard
  - moc
---

# Life Command Center

> *"The secret of getting ahead is getting started."* — Mark Twain

---

## Quick Navigation

| | | |
|---|---|---|
| [[LifeOS/05-Daily/\|Daily Notes]] | [[Task Management MOC]] | [[Goal Tracking MOC]] |
| [[Habit Dashboard MOC]] | [[Vision]] | [[Values]] |

---

## Today

### Tasks Due Today

```tasks
not done
due today
sort by priority
hide backlink
limit 10
```

### Scheduled Today

```tasks
not done
scheduled today
sort by priority
hide backlink
limit 5
```

---

## Active Projects

```dataview
TABLE WITHOUT ID
  file.link as "Project",
  priority as "Pri",
  "<progress value='" + progress + "' max='100'></progress>" as "Progress",
  due_date as "Due"
FROM "LifeOS/01-Projects"
WHERE status = "active"
SORT priority DESC, due_date ASC
LIMIT 8
```

[[LifeOS/01-Projects/|View All Projects]]

---

## Goal Progress

```dataview
TABLE WITHOUT ID
  file.link as "Goal",
  timeframe as "Period",
  "<progress value='" + metric_current + "' max='" + metric_target + "'></progress>" as "Progress",
  round((metric_current / metric_target) * 100, 0) + "%" as "%"
FROM "LifeOS/10-Goals"
WHERE type = "goal" AND status = "in-progress"
SORT timeframe ASC
LIMIT 5
```

[[Goal Tracking MOC|View All Goals]]

---

## This Week's Habits

```dataviewjs
const today = dv.date("today");
const weekStart = today.minus({days: today.weekday - 1});

const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => dv.date(p.file.name) >= weekStart);

const total = pages.length || 1;
const meditation = pages.where(p => p.meditation).length;
const exercise = pages.where(p => p.exercise).length;
const reading = pages.where(p => p.reading).length;
const journaling = pages.where(p => p.journaling).length;

const bar = (count, max) => {
  const pct = Math.round(count/max*100);
  return `<progress value="${count}" max="${max}"></progress> ${count}/${max}`;
};

dv.paragraph(`**Meditation:** ${bar(meditation, total)}`);
dv.paragraph(`**Exercise:** ${bar(exercise, total)}`);
dv.paragraph(`**Reading:** ${bar(reading, total)}`);
dv.paragraph(`**Journaling:** ${bar(journaling, total)}`);
```

[[Habit Dashboard MOC|View Habit Dashboard]]

---

## Upcoming Deadlines

```tasks
not done
due after today
due before in 14 days
sort by due
hide backlink
limit 8
```

---

## Recent Notes

```dataview
TABLE WITHOUT ID
  file.link as "Note",
  file.mday as "Modified"
FROM "LifeOS"
WHERE file.name != "_Home Dashboard"
SORT file.mday DESC
LIMIT 10
```

---

## Quick Capture

- [ ]

---

## Weekly Review

[[LifeOS/06-Weekly/|Open Weekly Reviews]] | Create: `Ctrl/Cmd + N` → Weekly Review template

---

*Last updated: `= date(today)`*
