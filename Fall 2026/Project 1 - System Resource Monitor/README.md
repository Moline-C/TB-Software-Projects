# Project 1 - System Resource Monitor

**Trailblazers Software Team - Fall 2026**

Build **TB System Resource Monitor**, a command-line Python application that reports how your computer's CPU, memory, and disk are being used, warns you when resources run high, shows which programs use the most memory, and saves snapshots to a log file.

**Start here: [TUTORIAL.md](./TUTORIAL.md)**

---

## Project Overview

Every operating system includes a tool like Task Manager on Windows, Activity Monitor on macOS, or `top` on Linux. In this project, you will build your own simplified version in Python.

This is the team's first project, designed for students who are new to Python and Git. The tutorial is **scaffolded**: most of the code structure is provided, and you complete the important pieces such as function calls, conditions, dictionary keys, loops, and error handling with guidance and hints at every step. You will test each feature as you build it.

When you finish, you will have a working, cross-platform program in your own public GitHub repository that you can show in your portfolio and on your resume.

---

## Learning Objectives

By completing this project, you will be able to:

- Create a GitHub repository, clone it into VS Code, use `git status`, `add`, `commit`, and `push`, and understand when to use `pull`
- Install and use a third-party Python library (`psutil`) with `pip` and `requirements.txt`
- Organize a program into multiple Python modules and import between them
- Write functions that take parameters and return values
- Use dictionaries and lists to organize related data
- Use conditionals (`if` / `elif` / `else`) to make decisions
- Use `for` loops to process collections and `while` loops to repeat actions
- Handle errors gracefully with `try` / `except`
- Read and write CSV files using Python's standard library
- Explain basic system concepts: CPU, RAM, disk storage, and processes
- Test code incrementally instead of all at the end
- Document a project with a professional README

---

## What You Are Building

A menu-driven command-line application:

```text
================================
    TB System Resource Monitor
================================
1. View Current System Status
2. Start Live Monitor
3. View Top Processes
4. Save Current Snapshot
5. View System Information
6. Exit
================================
Choose an option (1-6):
```

Example live monitor screen:

```text
==============================
   TB System Resource Monitor
==============================

CPU Usage:      34.2%
Memory Usage:   63.8%
Disk Usage:     71.4%

Status:
CPU:    OK
Memory: OK
Disk:   OK

Press Ctrl+C to stop monitoring.
```

---

## Required Features

Your submission must include all of the following:

| # | Feature | Requirements |
|---|---|---|
| 1 | **CPU Usage** | Display current CPU usage as a percentage |
| 2 | **Memory Usage** | Display memory percent, used memory in GB, and total memory in GB |
| 3 | **Disk Usage** | Display disk percent, used disk space in GB, and total disk space in GB for the main drive |
| 4 | **System Information** | Display operating system, computer name, and processor when available |
| 5 | **Resource Summary** | A function that returns all current values in a single dictionary |
| 6 | **Resource Warnings** | Warn when CPU exceeds 80%, memory exceeds 80%, or disk exceeds 90% |
| 7 | **Live Monitor** | Refresh the display every few seconds and stop cleanly with `Ctrl+C` |
| 8 | **Top Processes** | Show the top 5 processes by memory using PID, name, and memory percentage; skip processes that cannot be read without crashing |
| 9 | **Save Snapshot** | Append the current values with a timestamp to a CSV file in `logs/`, creating the header automatically |
| 10 | **Menu** | A menu loop with all six options; invalid input shows a friendly message |
| 11 | **Git History** | Multiple meaningful commits throughout the project instead of one commit at the end |
| 12 | **Personal README** | A README in your own repository describing your project |

The required project does **not** need administrator/root permissions and does not modify any system files.

---

## Technologies

| Tool | Purpose |
|---|---|
| **Python 3.8+** | Programming language |
| **psutil** | Cross-platform library for CPU, memory, disk, and process information |
| **Python standard library** | `platform`, `socket`, `os`, `time`, `csv`, `datetime` |
| **Git** | Version control |
| **GitHub** | Hosting your public project repository |
| **VS Code** | Code editor and terminal |

Works on **Windows, macOS, and Linux**.

---

## Project Structure

Your personal repository, `tb-system-resource-monitor`, will be organized like this:

```text
tb-system-resource-monitor/
│
├── main.py            # Menu and user interaction
├── monitor.py         # System info, resource monitoring, warnings, live monitor, processes
├── logger.py          # Saving snapshots to CSV
│
├── logs/
│   └── .gitkeep       # Keeps the logs folder in Git
│
├── .gitignore
├── README.md          # Your personal project README
└── requirements.txt   # psutil
```

---

## Getting Started

Follow [**TUTORIAL.md**](./TUTORIAL.md) from beginning to end.

It walks you through:

1. Understanding the project and key terms
2. Creating your GitHub repository and cloning it into VS Code
3. Setting up Python and `psutil`
4. Building each feature with a test after every section
5. Connecting everything with a menu
6. Testing the full application
7. Writing your personal README and submitting

Work through it in order. Each Part depends on the previous one.

---

## Testing Expectations

Testing is part of the assignment, not an afterthought.

- **Test as you go.** The tutorial includes a short test after each feature. Do not move on until the test passes.
- Before submitting, complete the full testing checklist in the tutorial.
- Make sure:
  - Every menu option works
  - Invalid menu input shows a friendly message
  - The live monitor refreshes and stops with `Ctrl+C` without a traceback
  - Top processes display without crashing when some processes are inaccessible
  - Saved snapshots appear in `logs/snapshots.csv`
  - The CSV contains one header row, a timestamp, and CPU, memory, and disk values
  - Warning thresholds are restored to their default values of 80%, 80%, and 90%
- Be prepared to **demonstrate** your program and **explain** how any part of it works.

---

## AI Policy

AI tools may be used as a **learning and debugging tool**, for example to explain a concept, clarify an error message, or help you understand why your code is not working.

However, **you must understand and be able to explain any code you submit.**

You may be asked to walk through your code, explain what a function does, or make a small change on the spot.

Submitting code you cannot explain is not acceptable.

The goal of this project is for you to learn these skills, not just to have a working program.

---

## Optional Extensions

After the required project is **complete, tested, and pushed**, you may add optional features to make your project stand out.

Some ideas:

- System uptime
- CPU-per-core display
- Configurable warning thresholds
- Search or filter processes by name
- Repeated logging every X seconds
- Viewing historical snapshots from the CSV
- Exporting a text report
- Network upload and download usage
- Battery monitoring
- CPU-per-process usage
- Charts and graphs with `matplotlib`
- A Tkinter GUI or dashboard

See **Part 15** of the tutorial for hints.

These are **optional** and are not required for submission.

Document any extensions you add in your personal README.

---

## Submission

1. Complete the project in your **personal public repository** named `tb-system-resource-monitor`.
2. Make sure all of your work is committed and pushed to GitHub.
3. Follow the instructions in [**Submissions/README.md**](./Submissions/README.md) to fork the central Trailblazers repository and submit your project through a pull request.

---

## Need Help?

- Check **Part 14: Troubleshooting** in the tutorial first.
- Read the error message carefully, especially the file name and line number.
- Ask a teammate or a project lead.
- Bring the exact error message and explain what you already tried.
