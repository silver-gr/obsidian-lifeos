---
type: project
status: active
priority: medium
due_date:
start_date: <% tp.file.creation_date("YYYY-MM-DD") %>
area: ""
goal: ""
progress: 0
estimated_hours: 0
actual_hours: 0
tags:
  - project
---

# <% tp.file.title %>

**Area:** `INPUT[suggester(optionQuery("LifeOS/02-Areas")):area]`
**Goal:** `INPUT[suggester(optionQuery("LifeOS/10-Goals")):goal]`
**Status:** `INPUT[inlineSelect(option(active), option(on-hold), option(completed), option(cancelled)):status]`
**Priority:** `INPUT[inlineSelect(option(high), option(medium), option(low)):priority]`

---

## Objective

<!-- What is the desired outcome? Why does this matter? -->


---

## Key Deliverables

- [ ] Deliverable 1
- [ ] Deliverable 2
- [ ] Deliverable 3

---

## Tasks

### Active Tasks
```tasks
not done
path includes {{query.file.path}}
sort by priority
hide backlink
```

### All Tasks
- [ ]

---

## Progress

<progress value="0" max="100"></progress> `VIEW[{progress}]`%

**Estimated:** `VIEW[{estimated_hours}]` hours | **Actual:** `VIEW[{actual_hours}]` hours

---

## Notes & Resources

### Meeting Notes


### Reference Links
-

### Related Files
```dataview
LIST
FROM [[]]
WHERE file.name != this.file.name
LIMIT 10
```

---

## Log

### <% tp.date.now("YYYY-MM-DD") %>

