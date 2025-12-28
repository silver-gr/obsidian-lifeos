---
type: goal
timeframe: 2025-Q1
status: planning
parent_goal: ""
metric_type: numeric
metric_target: 100
metric_current: 0
review_frequency: weekly
tags:
  - goal
  - okr
---

# <% tp.file.title %>

**Timeframe:** `INPUT[inlineSelect(option(2025-Q1), option(2025-Q2), option(2025-Q3), option(2025-Q4), option(2025)):timeframe]`
**Status:** `INPUT[inlineSelect(option(planning), option(in-progress), option(completed), option(abandoned)):status]`
**Parent Goal:** `INPUT[suggester(optionQuery("LifeOS/10-Goals")):parent_goal]`

---

## Objective

<!-- What do you want to achieve? Be specific and inspiring. -->


---

## Why This Matters

<!-- Connect to your values and vision. What will achieving this enable? -->


---

## Key Results

1. [ ] **KR1:**
2. [ ] **KR2:**
3. [ ] **KR3:**

---

## Progress

<progress value="`VIEW[{metric_current}]`" max="`VIEW[{metric_target}]`"></progress>

**Current:** `INPUT[number:metric_current]` / **Target:** `INPUT[number:metric_target]`

**Completion:** `VIEW[round((metric_current / metric_target) * 100, 0)]`%

---

## Active Projects

```dataview
TABLE WITHOUT ID
  file.link as "Project",
  status as "Status",
  progress + "%" as "Progress",
  due_date as "Due"
FROM "LifeOS/01-Projects"
WHERE contains(goal, this.file.name) OR contains(goal, this.file.link)
SORT due_date ASC
```

---

## Action Items

### This Week
```tasks
not done
path includes LifeOS
description includes <% tp.file.title %>
due before in 7 days
hide backlink
```

### All Tasks
- [ ]

---

## Weekly Review Notes

### Week of <% tp.date.now("YYYY-MM-DD") %>
**Progress:**

**Blockers:**

**Next Steps:**

---

## Milestones

| Milestone | Target Date | Status |
|-----------|-------------|--------|
|  |  | |

---

## Resources & References

-
