---
cssclass: dashboard
tags:
  - moc
  - habits
---

# Habit Dashboard

---

## Today's Habits

> Open today's daily note to toggle habits

[[LifeOS/05-Daily/|Open Daily Notes]]

---

## This Week's Progress

```dataviewjs
const today = dv.date("today");
const weekStart = today.minus({days: today.weekday - 1});

const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => dv.date(p.file.name) >= weekStart)
  .sort(p => p.file.name);

if (pages.length === 0) {
  dv.paragraph("*No daily notes this week yet.*");
} else {
  const total = pages.length;

  const habits = ['meditation', 'exercise', 'reading', 'journaling'];

  for (let habit of habits) {
    const count = pages.where(p => p[habit]).length;
    const pct = Math.round(count / total * 100);
    const emoji = pct >= 80 ? "🟢" : pct >= 50 ? "🟡" : "🔴";
    dv.paragraph(`${emoji} **${habit.charAt(0).toUpperCase() + habit.slice(1)}:** ${count}/${total} (${pct}%)`);
  }
}
```

---

## Weekly Habit Table

```dataview
TABLE WITHOUT ID
  file.link as "Day",
  choice(meditation, "✅", "❌") as "Med",
  choice(exercise, "✅", "❌") as "Exe",
  choice(reading, "✅", "❌") as "Read",
  choice(journaling, "✅", "❌") as "Jrn",
  sleep_hours as "Sleep",
  mood as "Mood"
FROM "LifeOS/05-Daily"
SORT file.name DESC
LIMIT 7
```

---

## Monthly Overview

```dataviewjs
const pages = dv.pages('"LifeOS/05-Daily"')
  .where(p => p.file.name.startsWith(dv.date("today").toFormat("yyyy-MM")))
  .sort(p => p.file.name);

if (pages.length === 0) {
  dv.paragraph("*No daily notes this month yet.*");
} else {
  const total = pages.length;

  dv.header(4, `${dv.date("today").toFormat("MMMM yyyy")} (${total} days tracked)`);

  const meditation = pages.where(p => p.meditation).length;
  const exercise = pages.where(p => p.exercise).length;
  const reading = pages.where(p => p.reading).length;
  const journaling = pages.where(p => p.journaling).length;

  dv.paragraph(`**Meditation:** <progress value="${meditation}" max="${total}"></progress> ${meditation}/${total}`);
  dv.paragraph(`**Exercise:** <progress value="${exercise}" max="${total}"></progress> ${exercise}/${total}`);
  dv.paragraph(`**Reading:** <progress value="${reading}" max="${total}"></progress> ${reading}/${total}`);
  dv.paragraph(`**Journaling:** <progress value="${journaling}" max="${total}"></progress> ${journaling}/${total}`);
}
```

---

## Habit Tracker Visualization

```tracker
searchType: frontmatter
searchTarget: meditation, exercise, reading, journaling
folder: LifeOS/05-Daily
datasetName: Meditation, Exercise, Reading, Journaling
month:
    color: green, blue, purple, orange
```

---

## Metrics Trends

### Sleep

```tracker
searchType: frontmatter
searchTarget: sleep_hours
folder: LifeOS/05-Daily
line:
    title: Sleep Hours
    yAxisLabel: Hours
    lineColor: blue
    yMin: 0
    yMax: 12
```

### Mood

```tracker
searchType: frontmatter
searchTarget: mood
folder: LifeOS/05-Daily
line:
    title: Mood
    yAxisLabel: Score
    lineColor: green
    yMin: 1
    yMax: 10
```

### Energy

```tracker
searchType: frontmatter
searchTarget: energy_level
folder: LifeOS/05-Daily
line:
    title: Energy Level
    yAxisLabel: Score
    lineColor: orange
    yMin: 1
    yMax: 10
```

---

## Habit Definitions

```dataview
TABLE WITHOUT ID
  file.link as "Habit",
  category as "Category",
  frequency as "Frequency"
FROM "LifeOS/11-Habits"
WHERE type = "habit"
SORT category ASC
```

[[LifeOS/11-Habits/|Manage Habits]]

---

## Yearly Heatmap

> Requires Heatmap Calendar plugin

```dataviewjs
// This will render with Heatmap Calendar plugin
const calendarData = {
    colors: {
        green: ["#c6e48b", "#7bc96f", "#49a648", "#2e8b32", "#196127"]
    },
    entries: []
};

for (let page of dv.pages('"LifeOS/05-Daily"')) {
    const habitCount = (page.meditation ? 1 : 0) +
                       (page.exercise ? 1 : 0) +
                       (page.reading ? 1 : 0) +
                       (page.journaling ? 1 : 0);

    if (page.file.name.match(/^\d{4}-\d{2}-\d{2}$/)) {
        calendarData.entries.push({
            date: page.file.name,
            intensity: habitCount,
            content: await dv.span(`[[${page.file.name}]]`)
        });
    }
}

renderHeatmapCalendar(this.container, calendarData);
```

---

[[_Home Dashboard|Back to Home]]
