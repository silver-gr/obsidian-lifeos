---
cssclass: dashboard
tags:
  - moc
  - tasks
---

# Task Management

---

## Quick Actions

| Today | This Week | Overdue |
|-------|-----------|---------|
| [[#Due Today]] | [[#This Week]] | [[#Overdue]] |

---

## Due Today

```tasks
not done
due today
sort by priority
hide backlink
```

---

## Scheduled Today

```tasks
not done
scheduled today
sort by priority
hide backlink
```

---

## This Week

```tasks
not done
due after yesterday
due before in 7 days
sort by due
sort by priority
hide backlink
```

---

## Overdue

```tasks
not done
due before today
sort by due
hide backlink
```

---

## By Priority

### High Priority

```tasks
not done
priority is high
sort by due
hide backlink
limit 15
```

### Medium Priority

```tasks
not done
priority is medium
sort by due
hide backlink
limit 10
```

---

## By Project

```tasks
not done
path includes 01-Projects
group by filename
sort by due
hide backlink
```

---

## By Area

### Health
```tasks
not done
path includes 02-Areas/Health
hide backlink
```

### Career
```tasks
not done
path includes 02-Areas/Career
hide backlink
```

### Learning
```tasks
not done
path includes 02-Areas/Learning
hide backlink
```

---

## Waiting For

```tasks
not done
description includes #waiting
hide backlink
```

---

## Someday/Maybe

```tasks
not done
path includes 04-Archives
hide backlink
limit 10
```

---

## Recently Completed

```tasks
done after 7 days ago
sort by done reverse
short mode
hide backlink
limit 20
```

---

## Task Statistics

```dataviewjs
const pages = dv.pages('"LifeOS"');
let totalTasks = 0;
let completedTasks = 0;

for (let page of pages) {
  const tasks = page.file.tasks;
  totalTasks += tasks.length;
  completedTasks += tasks.where(t => t.completed).length;
}

const pendingTasks = totalTasks - completedTasks;
const completionRate = totalTasks > 0 ? Math.round(completedTasks / totalTasks * 100) : 0;

dv.paragraph(`**Total Tasks:** ${totalTasks}`);
dv.paragraph(`**Completed:** ${completedTasks}`);
dv.paragraph(`**Pending:** ${pendingTasks}`);
dv.paragraph(`**Completion Rate:** ${completionRate}%`);
```

---

[[_Home Dashboard|Back to Home]]
