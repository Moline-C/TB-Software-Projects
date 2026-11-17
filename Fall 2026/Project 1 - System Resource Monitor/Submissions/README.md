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

## Part 6 - Create Your Submission Branch

Do not make your submission directly on your fork's `main` branch.

Create a new branch specifically for your Project 1 submission.

Use this format:

```text
firstname-lastname-project1
```

Example:

```bash
git checkout -b maya-smith-project1
```

Replace `maya-smith` with your own name.

Check that you are on the correct branch:

```bash
git branch
```

You should see an asterisk `*` beside your new branch.

Example:

```text
  main
* maya-smith-project1
```

---

## Part 7 - Find the Project 1 Submissions Folder

Inside your cloned Trailblazers repository, navigate to:

```text
Fall 2026/
└── Project 1 - System Resource Monitor/
    └── Submissions/
```

Inside the `Submissions` folder, create a folder using your name.

Use this format:

```text
First-Last
```

Example:

```text
Maya-Smith
```

Your folder should look like:

```text
Fall 2026/
└── Project 1 - System Resource Monitor/
    └── Submissions/
        └── Maya-Smith/
```

Do not put your files directly inside the main `Submissions` folder.

Every member should have their own folder.

---

## Part 8 - Copy Your Project Files Into Your Submission Folder

Now open your completed personal `system-resource-monitor` project.

Copy your project files into your personal Trailblazers submission folder.

Your submission should look similar to:

```text
Maya-Smith/
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

If you added optional files that are part of your project, you may include those as well.

For example:

```text
screenshots/
```

if your README uses screenshots.

---

## Part 9 - Do NOT Copy Generated or Personal Files

Before committing, make sure you did not copy files such as:

```text
scratch.py
logs/snapshots.csv
__pycache__/
*.pyc
.vscode/
.venv/
venv/
.DS_Store
Thumbs.db
```

Your submission should contain your project source code and documentation, not temporary files created by your computer.

Your `logs/` folder should normally contain only:

```text
.gitkeep
```

---

## Part 10 - Check Your Submission README

Your submission should include the `README.md` from your personal project repository.

Make sure your README includes:

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

Also include a link to your personal GitHub repository.

Example:

```markdown
## Personal Project Repository

[View My Project on GitHub](https://github.com/YOUR-USERNAME/system-resource-monitor)
```

Replace `YOUR-USERNAME` with your actual GitHub username.

Test the link before submitting.

---

## Part 11 - Check Your Changes

From the root of your cloned Trailblazers repository, open the terminal and run:

```bash
git status
```

Look carefully at the files Git says you changed.

Your new files should only be inside:

```text
Fall 2026/Project 1 - System Resource Monitor/Submissions/YOUR-NAME/
```

For example:

```text
Fall 2026/Project 1 - System Resource Monitor/Submissions/Maya-Smith/
```

You should not be changing:

```text
Project 1 - System Resource Monitor/README.md
Project 1 - System Resource Monitor/TUTORIAL.md
Project 1 - System Resource Monitor/Submissions/README.md
another student's submission
Fall 2026/README.md
the main repository README
```

If you accidentally changed something outside your submission folder, fix it before continuing.

---

## Part 12 - Stage Your Submission

Once everything looks correct, run:

```bash
git add .
```

Then check your changes again:

```bash
git status
```

Make sure the files listed are only the ones you intended to submit.

---

## Part 13 - Commit Your Submission

Create a clear commit describing what you are submitting.

Example:

```bash
git commit -m "Add Maya Smith Project 1 submission"
```

Replace `Maya Smith` with your own name.

A commit is a saved checkpoint of your changes.

---

## Part 14 - Push Your Submission Branch

Push your Project 1 branch to your fork on GitHub.

Example:

```bash
git push -u origin maya-smith-project1
```

Replace the branch name with the branch you created earlier.

The `-u` connects your local branch to the matching branch on GitHub.

After the first push, future pushes from that branch can usually be done with:

```bash
git push
```

---

## Part 15 - Open Your Fork on GitHub

Go to:

```text
github.com/YOUR-USERNAME/TB-Software-Projects
```

You may see a message near the top of the repository saying:

```text
Compare & pull request
```

Click it.

If you do not see that button:

1. Click **Pull requests**
2. Click **New pull request**
3. Choose your Project 1 branch

---

## Part 16 - Check the Pull Request Direction

This step is important.

Your pull request should go:

```text
Your Fork
Your Project 1 Branch

        ↓

Original Trailblazers Repository
main
```

The **base repository** should be the original:

```text
TB-Software-Projects
```

The **base branch** should be:

```text
main
```

The **compare repository** should be your fork.

The **compare branch** should be your Project 1 branch.

Example:

```text
base:
TB-Software-Projects / main

compare:
YOUR-USERNAME / maya-smith-project1
```

Do not create a pull request from your branch into your own fork's `main` branch.

The goal is to submit your work back to the original Trailblazers repository.

---

## Part 17 - Name Your Pull Request

Use this title format:

```text
Project 1 - First Last
```

Example:

```text
Project 1 - Maya Smith
```

Keep the title simple and consistent.

---

## Part 18 - Complete the Pull Request Description

Use the pull request template provided by the repository.

Before submitting, confirm:

- Your project works
- Your personal repository is public
- Your personal README is complete
- Your Trailblazers submission is inside your own folder
- Your personal repository link works
- Your required files are included
- Your generated CSV files are not included
- You did not upload temporary or cache files
- You understand the code you submitted

If you added optional features, you may mention them in the notes section.

---

## Part 19 - Create the Pull Request

Once everything is correct, click:

```text
Create pull request
```

Your Project 1 submission has now been sent for review.

Do not merge your own pull request.

The Software Director will review the submission before it is added to the Trailblazers repository.

---

## Part 20 - If Changes Are Requested

If you are asked to fix something, do not create a new pull request.

Go back to the same Project 1 branch on your computer.

Make the requested changes.

Then run:

```bash
git status
```

Stage the changes:

```bash
git add .
```

Commit them:

```bash
git commit -m "Address Project 1 review feedback"
```

Then push again:

```bash
git push
```

Your existing pull request will update automatically.

You do not need to open another pull request.

---

## Part 21 - If Your Fork Is Behind the Trailblazers Repository

Other students may have submissions merged while you are working.

If GitHub says your fork or branch is behind the original Trailblazers repository, update your fork before making additional changes.

The easiest option is usually through GitHub.

Open your fork and click:

```text
Sync fork
```

Then choose:

```text
Update branch
```

After updating the fork on GitHub, return to VS Code and run:

```bash
git checkout main
```

Then:

```bash
git pull
```

After `main` is updated, return to your submission branch:

```bash
git checkout firstname-lastname-project1
```

For your first Project 1 submission, you may not need to do this unless GitHub tells you your fork is behind.

---

## Browser-Only Submission Option

If you cannot use the Git command line for the submission process, you may complete the submission through GitHub's website.

You should still complete your actual project in your personal `system-resource-monitor` repository first.

### Step 1 - Fork the Repository

Open:

```text
TB-Software-Projects
```

Click:

```text
Fork
```

Create the fork under your GitHub account.

---

### Step 2 - Create a Submission Branch

Inside your fork, create a branch using:

```text
firstname-lastname-project1
```

Do not upload your submission directly to `main`.

---

### Step 3 - Navigate to the Submission Folder

Go to:

```text
Fall 2026/
Project 1 - System Resource Monitor/
Submissions/
```

---

### Step 4 - Create Your Personal Folder

Create:

```text
First-Last/
```

Example:

```text
Maya-Smith/
```

---

### Step 5 - Upload Your Project Files

Upload the files from your completed System Resource Monitor project.

Your folder should look similar to:

```text
Maya-Smith/
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

Do not upload:

```text
scratch.py
logs/*.csv
__pycache__/
*.pyc
.vscode/
.venv/
venv/
```

---

### Step 6 - Commit the Uploaded Files

Commit the files to your Project 1 branch.

Use a message such as:

```text
Add Maya Smith Project 1 submission
```

---

### Step 7 - Open a Pull Request

Open a pull request from:

```text
YOUR FORK / your-project1-branch
```

into:

```text
TB-Software-Projects / main
```

Use this pull request title:

```text
Project 1 - Your Name
```

Then create the pull request.

---

# Final Submission Checklist

Before submitting your pull request, confirm:

- [ ] My System Resource Monitor works.
- [ ] I tested all required features.
- [ ] My project is pushed to my personal GitHub repository.
- [ ] My personal repository is public.
- [ ] My personal repository has a complete README.
- [ ] My README explains what the project does.
- [ ] My README explains how to install and run the project.
- [ ] My README links correctly to any screenshots or demos I included.
- [ ] My Trailblazers submission is inside my own `First-Last` folder.
- [ ] My submission includes my source code.
- [ ] My submission includes `requirements.txt`.
- [ ] My submission includes `.gitignore`.
- [ ] My submission README links to my personal GitHub repository.
- [ ] I did not upload `scratch.py`.
- [ ] I did not upload generated CSV log files.
- [ ] I did not upload `__pycache__`.
- [ ] I did not upload `.venv` or `venv`.
- [ ] I did not modify another student's submission.
- [ ] I did not modify the Trailblazers project instructions.
- [ ] My pull request is going to the original Trailblazers repository.
- [ ] My pull request is targeting the `main` branch.
- [ ] I can explain the code I submitted.

---

# Need Help?

If you have trouble with:

- Forking
- Cloning
- Branches
- Git commands
- Push errors
- Pull requests
- Merge conflicts
- Repository structure
- Project submission

Ask in the Trailblazers Software Team GroupMe or bring the issue to a Software Team meeting.

When asking for help, include:

```text
1. What operating system are you using?
2. What command did you run?
3. What exact error message did you receive?
4. What have you already tried?
```

Do not wait until the submission deadline to ask for help.

