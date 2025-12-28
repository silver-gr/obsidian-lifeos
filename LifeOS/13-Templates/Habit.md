---
type: habit
category: health
frequency: daily
target_per_day: 1
current_streak: 0
best_streak: 0
start_date: <% tp.file.creation_date("YYYY-MM-DD") %>
tags:
  - habit
---

# <% tp.file.title %>

**Category:** `INPUT[inlineSelect(option(health), option(productivity), option(learning), option(mindfulness), option(social), option(creative)):category]`
**Frequency:** `INPUT[inlineSelect(option(daily), option(weekly), option(weekdays), option(custom)):frequency]`

---

## Why This Matters

<!-- Connect this habit to your values and goals. Why is this important? -->


---

## Implementation Intention

**Trigger (When/Where):**


**Routine (Exact Steps):**


**Reward (What makes it satisfying):**


---

## Tracking

### Last 30 Days

```dataviewjs
const habitKey = dv.current().file.name.toLowerCase().replace(/\s+/g, '_');
const pages = dv.pages('"LifeOS/05-Daily"')
  .sort(p => p.file.name, 'desc')
  .limit(30);

let completed = 0;
let total = pages.length;

for (let page of pages) {
  // Check common habit property names
  if (page.meditation || page.exercise || page.reading || page.journaling) {
    completed++;
  }
}

dv.paragraph(`**Completion Rate:** ${completed}/${total} (${Math.round(completed/total*100)}%)`);
```

### Streak History

```tracker
searchType: frontmatter
searchTarget: <% tp.file.title.toLowerCase().replace(/\s+/g, '_') %>
folder: LifeOS/05-Daily
datasetName: <% tp.file.title %>
month:
    color: green
```

---

## Progress Chart

```tracker
searchType: frontmatter
searchTarget: <% tp.file.title.toLowerCase().replace(/\s+/g, '_') %>
folder: LifeOS/05-Daily
line:
    title: <% tp.file.title %> Over Time
    yAxisLabel: Done
    lineColor: green
```

---

## Obstacles & Solutions

| Obstacle | Solution |
|----------|----------|
|  |  |

---

## Notes & Reflections


---

## Related Goals

```dataview
LIST
FROM "LifeOS/10-Goals"
WHERE contains(file.outlinks, this.file.link)
```
