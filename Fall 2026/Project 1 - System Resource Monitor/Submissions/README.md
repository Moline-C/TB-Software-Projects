# Project 1 - System Resource Monitor Submission Instructions

For Project 1, you will submit the link to your completed personal GitHub repository.

You do **not** need to copy your project files into the Trailblazers repository.

Your personal GitHub repository is the version you should keep polished for your resume, portfolio, internship applications, and future development.

---

## Before You Submit

Make sure your System Resource Monitor is complete and tested.

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
- A completed README

You should also be able to explain the code you submitted.

---

## Your Repository

Your personal repository should be named:

```text
system-resource-monitor
```

Your repository should look similar to:

```text
system-resource-monitor/
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

If you added optional features, you may have additional files.

---

## Make Sure Your Repository Is Public

Before submitting, open your repository on GitHub and make sure it is:

```text
Public
```

If the repository is private, the Software Team will not be able to review it.

---

## Check Your README

Your personal `README.md` should explain your project clearly.

It should include:

- Project title
- Project overview
- Features
- Technologies used
- Project structure
- Installation instructions
- How to run the program
- Menu options
- Screenshots or demo if applicable
- Known limitations
- Optional features you added
- What you learned

Your README should describe **your project**, not simply copy the Trailblazers assignment instructions.

---

## Check Your Git History

Your repository should show multiple meaningful commits.

Examples:

```text
Set up project structure
Add system information functions
Add CPU memory and disk monitoring
Add resource warnings
Add live monitoring
Add top process display
Add CSV snapshot logging
Add main menu
Complete project README
```

Do not wait until the end and upload the entire project in one commit.

Your Git history should show how your project developed over time.

---

## Files You Should NOT Submit

Do not upload generated or personal files such as:

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

Your `.gitignore` should prevent most of these files from being tracked.

---

## Final Test

Before submitting your repository link, run your program one more time.

Make sure:

- CPU usage displays correctly
- Memory usage displays correctly
- Disk usage displays correctly
- System information displays
- Resource warnings work
- Live monitoring works
- `Ctrl+C` stops the live monitor cleanly
- Top processes display
- CSV snapshots save correctly
- The menu works
- Invalid menu input does not crash the program
- Your README displays correctly on GitHub

---

## Push Your Final Changes

Before submitting, make sure your latest work is actually on GitHub.

In VS Code, run:

```bash
git status
```

If you still have changes, stage them:

```bash
git add .
```

Commit them:

```bash
git commit -m "Complete Project 1"
```

Then push:

```bash
git push
```

Open your repository on GitHub and confirm that your latest changes are visible.

If your files only exist in VS Code and are not visible on GitHub, your submission is not complete.

---

## What To Submit

Submit:

```text
Your Name
Your GitHub Repository Link
```

Example:

```text
Maya Smith
https://github.com/mayasmith/system-resource-monitor
```

Only submit the link to your **personal System Resource Monitor repository**.

Do not submit:

- A link to your GitHub profile
- A link to the Trailblazers repository
- A local file path from your computer
- A ZIP file unless specifically requested
- A screenshot instead of the repository link

The submitted link should open directly to your completed project repository.

---

# Final Submission Checklist

Before submitting, confirm:

- [ ] My System Resource Monitor works.
- [ ] I tested all required features.
- [ ] My repository is public.
- [ ] My latest code is pushed to GitHub.
- [ ] My README is complete.
- [ ] My README explains how to install and run the project.
- [ ] My repository has multiple meaningful commits.
- [ ] My repository includes `requirements.txt`.
- [ ] My repository includes `.gitignore`.
- [ ] I did not upload generated CSV logs.
- [ ] I did not upload `scratch.py`.
- [ ] I did not upload cache or virtual-environment files.
- [ ] The repository link I am submitting works.
- [ ] I can explain the code I submitted.

---

## Need Help?

If you run into a problem before submitting, ask in the Trailblazers Software Team GroupMe or bring the issue to a Software Team meeting.

When asking for help, include:

```text
1. What operating system are you using?
2. What command did you run?
3. What exact error message did you receive?
4. What have you already tried?
```
