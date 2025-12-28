---
cssclass: dashboard
tags:
  - moc
  - goals
---

# Goal Tracking

---

## Vision & Values

| [[Vision]] | [[Values]] |
|------------|------------|

---

## Current Quarter Goals

```dataview
TABLE WITHOUT ID
  file.link as "Goal",
  status as "Status",
  "<progress value='" + metric_current + "' max='" + metric_target + "'></progress>" as "Progress",
  round((metric_current / metric_target) * 100, 0) + "%" as "%"
FROM "LifeOS/10-Goals"
WHERE type = "goal" AND contains(timeframe, "Q1")
SORT metric_current DESC
```

---

## All Active Goals

```dataview
TABLE WITHOUT ID
  file.link as "Goal",
  timeframe as "Period",
  status as "Status",
  "<progress value='" + metric_current + "' max='" + metric_target + "'></progress>" as "Progress",
  round((metric_current / metric_target) * 100, 0) + "%" as "%"
FROM "LifeOS/10-Goals"
WHERE type = "goal" AND (status = "in-progress" OR status = "planning")
SORT timeframe ASC
```

---

## Goals by Quarter

### Q1 2025
```dataview
LIST
FROM "LifeOS/10-Goals/2025/Q1"
WHERE type = "goal"
```

### Q1 2026
```dataview
LIST
FROM "LifeOS/10-Goals/2026/Q1"
WHERE type = "goal"
```

### Q2 2026
```dataview
LIST
FROM "LifeOS/10-Goals/2026/Q2"
WHERE type = "goal"
```

### Q2 2025
```dataview
LIST
FROM "LifeOS/10-Goals/2025/Q2"
WHERE type = "goal"
```

### Q3 2025
```dataview
LIST
FROM "LifeOS/10-Goals/2025/Q3"
WHERE type = "goal"
```

### Q4 2025
```dataview
LIST
FROM "LifeOS/10-Goals/2025/Q4"
WHERE type = "goal"
```

---

## Projects Supporting Goals

```dataview
TABLE WITHOUT ID
  file.link as "Project",
  goal as "Supporting Goal",
  status as "Status",
  progress + "%" as "Progress"
FROM "LifeOS/01-Projects"
WHERE goal != null AND goal != ""
SORT goal ASC
```

---

## Completed Goals

```dataview
TABLE WITHOUT ID
  file.link as "Goal",
  timeframe as "Period",
  file.mday as "Completed"
FROM "LifeOS/10-Goals"
WHERE type = "goal" AND status = "completed"
SORT file.mday DESC
LIMIT 10
```

---

## Goal Review Schedule

| Review Type | Frequency | Next Due |
|-------------|-----------|----------|
| Goal Check-in | Weekly | [[LifeOS/06-Weekly/\|Weekly Review]] |
| Goal Deep Dive | Monthly | [[LifeOS/07-Monthly/\|Monthly Review]] |
| Goal Setting | Quarterly | [[LifeOS/08-Quarterly/\|Quarterly Review]] |

---

## Quick Add Goal

To create a new goal:
1. Navigate to `LifeOS/10-Goals/2025/Q1/` (or appropriate quarter)
2. Create new note with Goal template
3. Fill in objective and key results

---

[[_Home Dashboard|Back to Home]]
