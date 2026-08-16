# taskview - Project and Tasks Viewer

![HTML](https://img.shields.io/badge/HTML-single--file-blue)
![License](https://img.shields.io/badge/license-MIT-informational)
![Status](https://img.shields.io/badge/status-active-success)
![Platform](https://img.shields.io/badge/platform-any%20modern%20browser-lightgrey)
![Dependencies](https://img.shields.io/badge/deps-none-important)

A **self-contained viewer of projects and related tasks** that runs entirely in a single HTML file. No build step, server, or accounts necessary. Everything is saved to your browser's local storage on the device you open it on.

---

## Logo

<div align="center">
<img src="./assets/logo.svg" alt="taskview logo" width="200" style="background-color:#E7E9EF; padding: 24px; border-radius: 6px;">
</div>

## How it works

Open `taskview.html` in a browser and it renders a board of **projects**, each of which can be expanded to reveal its own list of **tasks**. Every project and task carries an importance level, a completion percentage, and an optional due date. A project with tasks has its completion and importance **automatically averaged** from those tasks; a project with no tasks yet is set by hand.

State is kept in the browser's `localStorage` (or, when the page is opened inside a Claude artifact, via the artifact's own storage API) and written back on every change, debounced by 250ms so rapid edits don't thrash storage.

> [!WARNING]
> **State lives only in the browser that saved it.** There is no cloud sync and no account. Opening the file on a different device or in a different browser starts from an empty board unless you import a backup. Use the built-in **Export** to keep a JSON copy somewhere safe.

---

## Features

- **Single file, zero install**: one `.html` file, no dependencies, build tools, offline
- **Projects and tasks**: expandable projects, each holding its own list of tasks
- **Automatic rollups**: a project's completion and importance averaged from its tasks
- **Four-level importance**: click the pips to cycle a project or task through importance levels 1-4
- **Due dates**: typed as `YYYY-MM-DD`, with a live countdown and a highlight for anything late
- **Grouping**: tag projects with an area to group and sort them independently
- **Flexible sorting**: sort by attention, due date, completion, importance, name, or manual order
- **Notes**: attach a free-text note to any project or task
- **Filtering**: live text filter across project names, task names, notes, and areas
- **Completed section**: finished projects fade out of the active board into a collapsible section
- **Backup and restore**: export to a JSON file, copy as text, or import/restore from a pasted backup
- **Editable title**: the board title is inline-editable and used to name exported backup files

---

## Installation

There is nothing to install. `taskview.html` is a static, self-contained file.

### 1. Clone the repository

```bash
git clone https://github.com/alandella/taskview.git
cd taskview
```

### 2. Open it

Double-click `taskview.html`, or open it from your browser with `File > Open`:

```bash
# macOS
open taskview.html

# Windows (PowerShell)
start taskview.html

# Linux
xdg-open taskview.html
```

No server, no dependencies, no build step required.

---

## Quickstart

1. Open `taskview.html` in your browser.
2. Type a project name into **Add a project** and press Enter.
3. Click the project row to expand it, then add tasks the same way.
4. Click the importance pips to set a level and type a due date as `YYYY-MM-DD`.
5. Do the work, and drag the slider to set completion. 
6. Everything saves automatically as you type.

---

## Usage

### Board basics

| Action | How |
|---|---|
| Add a project | Type into the **Add a project** field at the bottom of the board, press Enter |
| Add a task | Click a project to expand it, type into **Add a task**, press Enter |
| Collapse a project | Click anywhere on its row |
| Set importance | Click the importance pips (cycles 1 → 2 → 3 → 4 → 1) |
| Set completion | Drag the slider, or click the checkbox to jump to 100% / 0% |
| Set a due date | Type directly into the due date field, as `YYYY-MM-DD` |
| Reorder | Click the down arrow to move a row one place down |
| Group by area | Type an area name into the area field next to an ungrouped project |
| Add a note | Click **note** on a project or task row |
| Filter the board | Type into the filter box; matches names, notes, and areas |
| Rename the board | Click the title at the top and edit it inline |
| Delete a row | Click the &times; button, then click again to confirm |

> [!NOTE]
> Importance and completion on a project are only editable directly while it has no tasks. As soon as a task is added, both values roll up automatically from that project's tasks.

### Sorting

Each area group has its own **Sort** menu:

| Sort mode | Orders by |
|---|---|
| Needs attention | Importance plus deadline pressure (default) |
| Due date | Soonest due date first, undated last |
| Least done | Lowest completion first |
| Importance | Highest importance first |
| Name | Alphabetical |
| My order | Manual order, set by dragging rows down with the &darr; button |

Switching away from **My order** and back again re-freezes the current on-screen order as the new manual order.

---

## Backup and restore

Board data lives only in local browser storage, so the **Backup** panel at the bottom of the page is the way to move data between browsers, devices, or backups.

| Action | Result |
|---|---|
| Export | Downloads a timestamped JSON file and fills the text box with the same content |
| Copy text | Copies the current backup JSON to the clipboard |
| Import file | Loads a `.json` file into the text box (does not apply it yet) |
| Restore | Applies the JSON currently in the text box, replacing the board |

> [!WARNING]
> **Restore replaces the entire board.** There is no undo beyond whatever backup you made beforehand. Export before restoring if you want to keep the current state as a fallback.

Example backup shape:

```json
{
  "v": 1,
  "title": "Projects",
  "projects": [
    {
      "id": "a1b2c3d",
      "name": "Website redesign",
      "importance": 3,
      "due": "2026-09-01",
      "area": "Work",
      "note": "",
      "tasks": [
        { "id": "e4f5g6h", "name": "Wireframes", "importance": 2, "done": 60, "due": "2026-08-25" }
      ]
    }
  ]
}
```

---

## Storage model

| Environment | Backend used |
|---|---|
| Opened inside a Claude artifact | Claude's artifact storage API |
| Opened as a local file | Browser `localStorage` |

> [!TIP]
> Because storage is scoped to the browser (and, for local files, sometimes to the exact file path), keep a recent export handy if you rely on this across multiple machines or browser profiles. In addition, if a private browser is used, a warning banner appears and **Export** is the only way to keep your data.

---

## Dependencies

None. `taskview.html` uses only vanilla HTML, CSS, and JavaScript, with no external scripts, stylesheets, or fonts.

---

## Contributing

Pull requests are welcome.
For major changes, please open an issue first to discuss what you would like to change or add.

---

## License

Distributed under the **MIT License**. See the [`LICENSE`](LICENSE) file for details.

&copy; 2026 Andrea Giuseppe Landella
