---
date: <% tp.file.title %>
type: monthly-review
tags:
  - monthly
  - review
month: <% tp.date.now("MMMM", 0, tp.file.title, "YYYY-MM") %>
year: <% tp.date.now("YYYY", 0, tp.file.title, "YYYY-MM") %>
---

# Monthly Review: <% tp.date.now("MMMM YYYY", 0, tp.file.title, "YYYY-MM") %>

<< [[<% tp.date.now("YYYY-MM", -1, tp.file.title, "YYYY-MM") %>]] | [[<% tp.date.now("YYYY-MM", 1, tp.file.title, "YYYY-MM") %>]] >>

---

## Month at a Glance

### Habit Summary

```dataviewjs
const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => p.file.name.startsWith("<% tp.file.title %>"));

const total = pages.length || 1;
const meditation = pages.where(p => p.meditation).length;
const exercise = pages.where(p => p.exercise).length;
const reading = pages.where(p => p.reading).length;
const journaling = pages.where(p => p.journaling).length;

dv.paragraph(`**Days Tracked:** ${total}`);
dv.paragraph(`**Meditation:** ${meditation}/${total} (${Math.round(meditation/total*100)}%)`);
dv.paragraph(`**Exercise:** ${exercise}/${total} (${Math.round(exercise/total*100)}%)`);
dv.paragraph(`**Reading:** ${reading}/${total} (${Math.round(reading/total*100)}%)`);
dv.paragraph(`**Journaling:** ${journaling}/${total} (${Math.round(journaling/total*100)}%)`);
```

### Average Metrics

```dataviewjs
const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => p.file.name.startsWith("<% tp.file.title %>"));

const total = pages.length || 1;
const avgSleep = pages.array().reduce((sum, p) => sum + (p.sleep_hours || 0), 0) / total;
const avgMood = pages.array().reduce((sum, p) => sum + (p.mood || 0), 0) / total;
const avgEnergy = pages.array().reduce((sum, p) => sum + (p.energy_level || 0), 0) / total;
const avgProd = pages.array().reduce((sum, p) => sum + (p.productivity || 0), 0) / total;

dv.paragraph(`**Average Sleep:** ${avgSleep.toFixed(1)} hours`);
dv.paragraph(`**Average Mood:** ${avgMood.toFixed(1)}/10`);
dv.paragraph(`**Average Energy:** ${avgEnergy.toFixed(1)}/10`);
dv.paragraph(`**Average Productivity:** ${avgProd.toFixed(1)}/10`);
```

---

## Weekly Reviews This Month

```dataview
TABLE WITHOUT ID
  file.link as "Week",
  file.cday as "Created"
FROM "LifeOS/06-Weekly"
WHERE file.name >= "<% tp.file.title %>-W01" AND file.name <= "<% tp.file.title %>-W53"
SORT file.name ASC
```

---

## Goal Progress

```dataview
TABLE WITHOUT ID
  file.link as "Goal",
  timeframe as "Period",
  "<progress value='" + metric_current + "' max='" + metric_target + "'></progress>" as "Progress",
  round((metric_current / metric_target) * 100, 0) + "%" as "%"
FROM "LifeOS/10-Goals"
WHERE type = "goal"
SORT timeframe ASC
```

---

## Projects Completed

```dataview
TABLE WITHOUT ID
  file.link as "Project",
  area as "Area",
  file.mday as "Completed"
FROM "LifeOS/01-Projects"
WHERE status = "completed"
  AND file.mday >= date("<% tp.file.title %>-01")
  AND file.mday <= date("<% tp.file.title %>-31")
SORT file.mday DESC
```

---

## Projects In Progress

```dataview
TABLE WITHOUT ID
  file.link as "Project",
  status as "Status",
  progress + "%" as "Progress",
  due_date as "Due"
FROM "LifeOS/01-Projects"
WHERE status = "active"
SORT due_date ASC
```

---

## Reflection

### Wins & Accomplishments


### Challenges & Lessons


### What to Start / Stop / Continue

**Start:**
-

**Stop:**
-

**Continue:**
-

---

## Next Month Focus

### Top 3 Priorities
1.
2.
3.

### Goals to Advance


### Habits to Improve


---

## Review Checklist

- [ ] Reviewed all weekly reviews
- [ ] Updated all goal progress metrics
- [ ] Archived completed projects
- [ ] Reviewed and updated Areas
- [ ] Set next month's priorities
