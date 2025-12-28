---
date: <% tp.file.title %>
type: weekly-review
tags:
  - weekly
  - review
week_number: <% tp.date.now("ww", 0, tp.file.title, "YYYY-[W]ww") %>
year: <% tp.date.now("YYYY", 0, tp.file.title, "YYYY-[W]ww") %>
---

# Weekly Review: <% tp.file.title %>

<< [[<% tp.date.now("YYYY-[W]ww", -7, tp.file.title, "YYYY-[W]ww") %>]] | [[<% tp.date.now("YYYY-[W]ww", 7, tp.file.title, "YYYY-[W]ww") %>]] >>

**Period:** <% tp.date.now("MMMM D", "monday", tp.file.title, "YYYY-[W]ww") %> - <% tp.date.now("MMMM D, YYYY", "sunday", tp.file.title, "YYYY-[W]ww") %>

---

## Habit Summary

```dataview
TABLE WITHOUT ID
  file.link as "Day",
  meditation as "Med",
  exercise as "Exe",
  reading as "Read",
  journaling as "Jrn",
  sleep_hours as "Sleep",
  mood as "Mood",
  energy_level as "Energy"
FROM "LifeOS/05-Daily"
WHERE file.name >= "<% tp.date.now('YYYY-MM-DD', 'monday', tp.file.title, 'YYYY-[W]ww') %>"
  AND file.name <= "<% tp.date.now('YYYY-MM-DD', 'sunday', tp.file.title, 'YYYY-[W]ww') %>"
SORT file.name ASC
```

### Habit Completion Rate

```dataviewjs
const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => p.file.name >= "<% tp.date.now('YYYY-MM-DD', 'monday', tp.file.title, 'YYYY-[W]ww') %>"
    && p.file.name <= "<% tp.date.now('YYYY-MM-DD', 'sunday', tp.file.title, 'YYYY-[W]ww') %>");

const total = pages.length || 1;
const meditation = pages.where(p => p.meditation).length;
const exercise = pages.where(p => p.exercise).length;
const reading = pages.where(p => p.reading).length;
const journaling = pages.where(p => p.journaling).length;

dv.paragraph(`**Meditation:** ${meditation}/${total} (${Math.round(meditation/total*100)}%)`);
dv.paragraph(`**Exercise:** ${exercise}/${total} (${Math.round(exercise/total*100)}%)`);
dv.paragraph(`**Reading:** ${reading}/${total} (${Math.round(reading/total*100)}%)`);
dv.paragraph(`**Journaling:** ${journaling}/${total} (${Math.round(journaling/total*100)}%)`);
```

---

## Tasks Completed

```tasks
done after <% tp.date.now("YYYY-MM-DD", "monday", tp.file.title, "YYYY-[W]ww") %>
done before <% tp.date.now("YYYY-MM-DD", 8, tp.file.title, "YYYY-[W]ww") %>
group by filename
short mode
hide backlink
```

---

## Overdue Tasks (Action Required)

```tasks
not done
due before <% tp.date.now("YYYY-MM-DD", "monday", tp.file.title, "YYYY-[W]ww") %>
sort by due
hide backlink
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
WHERE type = "goal" AND status = "in-progress"
SORT timeframe ASC
```

---

## Weekly Metrics Summary

```dataviewjs
const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => p.file.name >= "<% tp.date.now('YYYY-MM-DD', 'monday', tp.file.title, 'YYYY-[W]ww') %>"
    && p.file.name <= "<% tp.date.now('YYYY-MM-DD', 'sunday', tp.file.title, 'YYYY-[W]ww') %>");

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

## Reflection

### What Worked Well


### What Didn't Work


### Key Learnings


### Blockers & Challenges


---

## Next Week Planning

### Top 3 Priorities
1.
2.
3.

### Tasks to Carry Forward

```tasks
not done
scheduled before <% tp.date.now("YYYY-MM-DD", 8, tp.file.title, "YYYY-[W]ww") %>
hide backlink
limit 10
```

### Goals Focus


---

## Review Checklist

- [ ] Reviewed all daily notes
- [ ] Updated goal progress
- [ ] Processed inbox items
- [ ] Scheduled next week's tasks
- [ ] Archived completed projects
