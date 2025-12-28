---
date: <% tp.file.title %>
day: <% tp.date.now("dddd", 0, tp.file.title, "YYYY-MM-DD") %>
week: "[[<% tp.date.now('YYYY-[W]ww', 0, tp.file.title, 'YYYY-MM-DD') %>]]"
month: "[[<% tp.date.now('YYYY-MM', 0, tp.file.title, 'YYYY-MM-DD') %>]]"
tags:
  - daily
meditation: false
exercise: false
reading: false
journaling: false
water_glasses: 0
sleep_hours: 0
mood: 5
energy_level: 5
productivity: 5
---

# <% tp.file.title %>

<< [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>]] | [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>]] >>

---

## Focus

**Top 3 Priorities:**
1.
2.
3.

**Quarterly Goal Focus:**
![[Vision#Current Focus]]

---

## Tasks

### Due Today
```tasks
not done
due on <% tp.file.title %>
hide backlink
sort by priority
```

### Scheduled Today
```tasks
not done
scheduled on <% tp.file.title %>
hide backlink
sort by priority
```

### Quick Capture
- [ ]

---

## Habits

| Habit | Status |
|-------|--------|
| Meditation (20 min) | `INPUT[toggle:meditation]` |
| Exercise (30 min) | `INPUT[toggle:exercise]` |
| Reading (30 min) | `INPUT[toggle:reading]` |
| Journaling (10 min) | `INPUT[toggle:journaling]` |

**Water Intake:** `VIEW[{water_glasses}]` glasses `INPUT[inlineSelect(option(+1), option(+2), option(reset)):water_glasses]`

---

## Metrics

| Metric | Value |
|--------|-------|
| Sleep | `INPUT[number:sleep_hours]` hours |
| Mood | `INPUT[slider(minValue(1), maxValue(10)):mood]` |
| Energy | `INPUT[slider(minValue(1), maxValue(10)):energy_level]` |
| Productivity | `INPUT[slider(minValue(1), maxValue(10)):productivity]` |

---

## Log

### Morning


### Afternoon


### Evening


---

## Reflection

**Wins:**
-

**Gratitude:**
-

**Learnings:**
-

**Tomorrow's Priority:**
-
