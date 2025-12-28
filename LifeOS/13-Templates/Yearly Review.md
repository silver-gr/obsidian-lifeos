---
date: <% tp.file.title %>
type: yearly-review
tags:
  - yearly
  - review
year: <% tp.file.title %>
---

# Yearly Review: <% tp.file.title %>

<< [[<% parseInt(tp.file.title) - 1 %>]] | [[<% parseInt(tp.file.title) + 1 %>]] >>

---

## Executive Summary

**The Year in a Sentence:**


**Biggest Achievement:**


**Biggest Challenge:**


---

## The Year in Review

### Quarterly Progress

#### Q1
-

#### Q2
-

#### Q3
-

#### Q4
-

---

## Habit Analysis (Yearly)

```dataviewjs
const year = "<% tp.file.title %>";
const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => p.file.name.startsWith(year))
  .sort(p => p.file.name);

if (pages.length === 0) {
  dv.paragraph("*No data for this year.*");
} else {
  const total = pages.length;
  const habits = ['meditation', 'exercise', 'reading', 'journaling'];

  dv.header(3, `Consistency Across ${total} Days`);

  for (let habit of habits) {
    const count = pages.where(p => p[habit]).length;
    const pct = Math.round(count / total * 100);
    dv.paragraph(`**${habit.charAt(0).toUpperCase() + habit.slice(1)}:** ${count}/${total} (${pct}%)`);
  }
}
```

---

## Metric Trends

### Average Mood & Energy

```dataviewjs
const year = "<% tp.file.title %>";
const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => p.file.name.startsWith(year));

const total = pages.length || 1;
const avgMood = pages.array().reduce((sum, p) => sum + (p.mood || 0), 0) / total;
const avgEnergy = pages.array().reduce((sum, p) => sum + (p.energy_level || 0), 0) / total;
const avgSleep = pages.array().reduce((sum, p) => sum + (p.sleep_hours || 0), 0) / total;

dv.paragraph(`**Avg Mood:** ${avgMood.toFixed(1)}/10`);
dv.paragraph(`**Avg Energy:** ${avgEnergy.toFixed(1)}/10`);
dv.paragraph(`**Avg Sleep:** ${avgSleep.toFixed(1)} hours`);
```

---

## Goals Audit

### Completed Goals
```dataview
TABLE timeframe as "Period", metric_target as "Target", metric_current as "Result"
FROM "LifeOS/10-Goals"
WHERE type = "goal" AND status = "completed" AND contains(file.path, "<% tp.file.title %>")
```

### Unfinished Goals (The "Why")
```dataview
TABLE timeframe as "Period", status as "Status"
FROM "LifeOS/10-Goals"
WHERE type = "goal" AND status != "completed" AND contains(file.path, "<% tp.file.title %>")
```

---

## Deep Reflection

### What did I learn about myself?


### What was my best investment (time/money/energy)?


### What should I stop doing?


---

## Looking Ahead: 2026

**Focus Theme for Next Year:**


**Top 3 Objectives for 2026:**
1.
2.
3.

---

## Review Checklist

- [ ] Reviewed all 12 Monthly Reviews
- [ ] Updated Vision and Values
- [ ] Created 2026 Goal structure
- [ ] Cleaned up the "Inbox" and "Archives"
