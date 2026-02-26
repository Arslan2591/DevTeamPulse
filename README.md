# Dev Team Pulse v4

**Live Demo:** https://arslan2591.github.io/DevTeamPulse/

A lightweight, single-file web application that transforms Jira CSV exports into an interactive team capacity and workload dashboard. Built for engineering managers and team leads who need quick visibility into team health without complex tooling.

## Features

- **Capacity Analysis** — Calculates remaining workload per developer (hours/days) and categorizes status as Red/Yellow/Green
- **Anomaly Detection** — Flags 5 types of issues: overrun estimates, unlogged work, review bottlenecks, missing estimates, and depleted pipelines
- **Wins Tracking** — Surfaces merged/completed items from the last 2 weeks, grouped by week
- **Interactive Dashboard** — Summary cards, per-developer breakdowns, expandable issue tables, and direct Jira links
- **Zero Dependencies** — Pure HTML/CSS/JavaScript with no build tools, frameworks, or backend required
- **Drag-and-Drop Upload** — Simple CSV file upload with drag-and-drop or file browser

## Quick Start

1. **Export data from Jira** — Run this JQL in your Jira project:

   ```
   project = DEV AND (statusCategory in ("In Progress", "To Do") OR (status = Merged AND updated >= -14d)) ORDER BY assignee ASC, key ASC
   ```

   Then export the results as CSV.

2. **Open the app** — Open `index.html` in any modern browser.

3. **Upload the CSV** — Drag and drop the exported CSV file (or click to browse).

4. **View the report** — The dashboard renders immediately with capacity metrics, alerts, and wins.

## Dashboard Overview

The report includes:

| Section | Description |
|---------|-------------|
| Summary Cards | Developer count, low-capacity alerts, items in review, total anomalies, weekly wins |
| Developer Cards | Individual capacity bars, status breakdowns, alerts with Jira links, recent wins |
| Issues Table | Expandable per-developer table showing active items with estimates and time spent |

### Capacity Thresholds

| Status | Remaining Capacity |
|--------|-------------------|
| Red | Less than 2 days |
| Yellow | 2 to 5 days |
| Green | More than 5 days |

### Anomaly Types

| Anomaly | Trigger |
|---------|---------|
| Work Ratio > 100% | Estimate exceeded on an issue |
| No Time Logged | Issue has an estimate but zero time logged |
| Review Bottleneck | 2+ issues stuck in "In Review" status |
| Missing Estimate | Active issue has no time estimate |
| Pipeline Depleted | High ratio of Done vs Active items |

## Configuration

The app ships with defaults for the `aimyable.atlassian.net` Jira instance. To customize:

| Setting | Where to Change | Default |
|---------|----------------|---------|
| Jira domain | Search/replace `aimyable.atlassian.net` in `index.html` | `aimyable.atlassian.net` |
| Low capacity threshold | `analyzeData()` function | 2 days |
| Moderate capacity threshold | `analyzeData()` function | 5 days |
| Wins lookback window | `analyzeData()` function | 14 days |
| Working hours per day | `analyzeData()` function | 8 hours |
| Theme colors | CSS `:root` variables | Dark theme |

## Tech Stack

- **HTML5 / CSS3 / Vanilla JavaScript (ES6+)**
- **Google Fonts** — DM Sans, JetBrains Mono
- **No frameworks, no build step, no backend**

## Browser Support

Any modern browser with ES6+, FileReader API, and Clipboard API support (Chrome, Firefox, Safari, Edge).

## License

This project is proprietary.
