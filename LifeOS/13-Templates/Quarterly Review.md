---
date: <% tp.file.title %>
type: quarterly-review
tags:
  - quarterly
  - review
quarter: <% tp.file.title.split("-")[1] %>
year: <% tp.file.title.split("-")[0] %>
---

# Quarterly Review: <% tp.file.title %>

<< [[<% tp.date.now("YYYY-[Q]Q", -90, tp.file.title + "-01", "YYYY-[Q]Q") %>]] | [[<% tp.date.now("YYYY-[Q]Q", 90, tp.file.title + "-01", "YYYY-[Q]Q") %>]] >>

---

## Executive Summary

**The Quarter in a Sentence:**


**Top Achievement:**


**Primary Challenge:**


---

## Goal Review

### Goal Progress
```dataview
TABLE status, metric_current + "/" + metric_target as "Metric", round((metric_current/metric_target)*100) + "%" as "Progress"
FROM "LifeOS/10-Goals"
WHERE type = "goal" AND contains(timeframe, "<% tp.file.title.split("-")[1] %>") AND contains(timeframe, "<% tp.file.title.split("-")[0] %>")
```

### Wins & Milestones
-

### Missed Targets (Analysis)
-

---

## Habit Analysis

```dataviewjs
const quarter = "<% tp.file.title %>"; // e.g., 2025-Q1
const year = quarter.split("-")[0];
const q = parseInt(quarter.split("-")[1].replace("Q", ""));

// Calculate start and end months for the quarter
const startMonth = (q - 1) * 3 + 1;
const endMonth = startMonth + 2;

const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => {
    const day = dv.date(p.file.name);
    return day.year == year && day.month >= startMonth && day.month <= endMonth;
  });

const total = pages.length || 1;
const habits = ['meditation', 'exercise', 'reading', 'journaling'];

dv.header(3, `Consistency Across ${total} Days`);

for (let habit of habits) {
    const count = pages.where(p => p[habit]).length;
    const pct = Math.round(count / total * 100);
    dv.paragraph(`**${habit.charAt(0).toUpperCase() + habit.slice(1)}:** ${count}/${total} (${pct}%)`);
}
```

---

## Key Metrics

```dataviewjs
const quarter = "<% tp.file.title %>";
const year = quarter.split("-")[0];
const q = parseInt(quarter.split("-")[1].replace("Q", ""));
const startMonth = (q - 1) * 3 + 1;
const endMonth = startMonth + 2;

const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => {
    const day = dv.date(p.file.name);
    return day.year == year && day.month >= startMonth && day.month <= endMonth;
  });

const total = pages.length || 1;
const avgMood = pages.array().reduce((sum, p) => sum + (p.mood || 0), 0) / total;
const avgProd = pages.array().reduce((sum, p) => sum + (p.productivity || 0), 0) / total;

dv.paragraph(`**Average Mood:** ${avgMood.toFixed(1)}/10`);
dv.paragraph(`**Average Productivity:** ${avgProd.toFixed(1)}/10`);
```

---

## Retrospective

### Start / Stop / Continue
- **Start:**
- **Stop:**
- **Continue:**

### Life Domains Check-in
- **Health:**
- **Career:**
- **Finance:**
- **Relationships:**

---

## Next Quarter Planning

### Focus Theme:


### Top 3 Goals:
1.
2.
3.

### Key Projects
```dataview
TABLE status, due_date
FROM "LifeOS/01-Projects"
WHERE status = "planning" OR status = "active"
SORT due_date ASC
```

---

## Review Checklist

- [ ] Reviewed all Weekly Reviews for the quarter
- [ ] Updated Goal statuses
- [ ] Planned next quarter's goals
- [ ] Archived completed projects
