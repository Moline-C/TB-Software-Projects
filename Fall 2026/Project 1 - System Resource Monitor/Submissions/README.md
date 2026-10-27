# Project 1 - System Resource Monitor Submission Instructions

Each Software Team member will keep their completed System Resource Monitor project in **two places**:

1. Your own personal GitHub repository
2. The Trailblazers Software Projects repository

Your personal repository is the version you can use for your resume, portfolio, and job applications.

Your Trailblazers submission allows the Software Team to keep completed projects together in one central repository.

---

# Before You Submit

Make sure your project is complete and tested.

Your project should include:

- CPU usage
- Memory usage
- Disk usage
- System information
- Resource warnings
- Live monitoring
- Top processes
- CSV snapshot logging
- A working menu
- Multiple meaningful Git commits
- A completed personal README

Also make sure you understand the code you are submitting.

---

# Important: Files You Should NOT Submit

Do not submit generated or personal files such as:

```text
__pycache__/
*.pyc
.vscode/
scratch.py
logs/*.csv
.venv/
venv/
.DS_Store
Thumbs.db
```

Your `logs/` folder may contain:

```text
.gitkeep
```

but should not contain your generated CSV logs.

Your `.gitignore` should already prevent most of these files from being tracked.

---

# Part 1 - Complete Your Personal GitHub Repository

Before submitting to Trailblazers, your completed project should already be pushed to your own public GitHub repository.

Your personal repository should be named:

```text
tb-system-resource-monitor
```

It should look similar to:

```text
tb-system-resource-monitor/
│
├── main.py
├── monitor.py
├── logger.py
│
├── logs/
│   └── .gitkeep
│
├── .gitignore
├── README.md
└── requirements.txt
```

Your personal repository should NOT contain generated CSV logs or personal test files.

---

# Part 2 - Check Your Personal Repository

Open your personal repository on GitHub.

Make sure:

- Your latest code is pushed
- Your repository is public
- Your README is complete
- Your screenshot or demo displays correctly
- Your project files are visible
- Your generated CSV logs are not uploaded
- Your `scratch.py` file is not uploaded
- Your program runs correctly

Your personal README should explain:

- What your project does
- Features
- Technologies used
- Project structure
- Installation
- How to run the program
- Menu options
- Known limitations
- Optional features you added
- What you learned

---

# Part 3 - Fork the Trailblazers Repository

Now you will submit your project to the Trailblazers Software Projects repository.

Open the:

```text
TB-Software-Projects
```

repository.

In the top-right area of GitHub, click:

```text
Fork
```

Choose your own GitHub account.

Keep the repository name:

```text
TB-Software-Projects
```

Then click:

```text
Create fork
```

GitHub will create your own copy of the Trailblazers repository.

Your fork will look similar to:

```text
github.com/YOUR-USERNAME/TB-Software-Projects
```

The original Trailblazers repository is the main team repository.

Your fork is your personal copy where you can safely make your submission changes.

---

# Part 4 - Clone Your Fork

Open your fork:

```text
github.com/YOUR-USERNAME/TB-Software-Projects
```

Click the green:

```text
Code
```

button.

Make sure:

```text
HTTPS
```

is selected.

Copy the repository URL.

It should look similar to:

```text
https://github.com/YOUR-USERNAME/TB-Software-Projects.git
```

Open VS Code.

Press:

```text
Ctrl + Shift + P
```

On macOS:

```text
Command + Shift + P
```

Search for:

```text
Git: Clone
```

Choose:

```text
Git: Clone
```

Paste the URL to your fork.

Choose where you want to save it.

When VS Code asks whether you want to open the cloned repository, click:

```text
Open
```

---

# Part 5 - Confirm You Cloned Your Fork

Open the VS Code terminal.

Run:

```bash
git remote -v
```

You should see your GitHub username in the repository URL.

Example:

```text
origin  https://github.com/YOUR-USERNAME/TB-Software-Projects.git
```

This confirms you are working inside **your fork**, not directly inside the original Trailblazers repository.

---

# Part 6 - Create Your Submission Branch

Do not
