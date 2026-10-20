# Project 1 - Ad Blocker Submission Instructions

Each Software Team member will keep their completed Ad Blocker project in **two places**:

1. Your own personal GitHub repository
2. The Trailblazers Software Projects repository

Your personal repository is the version you can use for your resume, portfolio, and job applications.

Your Trailblazers submission allows us to keep a record of completed Software Team projects in one central location.

---

# Before You Submit

Your project should be complete and tested before submitting it to the Trailblazers repository.

Make sure:

- Your program runs
- Ad blocking can be enabled
- Ad blocking can be disabled
- Blocking status can be viewed
- Your blocklist works
- Your whitelist works
- Your custom blocklist works
- Your hosts file is backed up before changes
- Your restore feature works
- Existing hosts-file entries are preserved
- Your program handles common errors
- Your personal GitHub repository has a completed README
- You understand the code you are submitting

---

# Important: Files You Must NOT Submit

Do **not** upload personal hosts-file backups.

Do not submit:

```text
backups/hosts_original.bak
backups/hosts_*.bak
```

Also do not submit generated or personal development files such as:

```text
__pycache__/
*.pyc
.vscode/
.DS_Store
```

Your personal hosts file may contain information specific to your computer.

Never force-add backup files to Git if `.gitignore` is excluding them.

---

# Part 1 - Create Your Personal GitHub Repository

Before submitting to Trailblazers, your full project should be stored in your own GitHub repository.

A recommended repository name is:

```text
tb-ad-blocker
```

Your personal repository should contain something similar to:

```text
tb-ad-blocker/
│
├── main.py
├── blocker.py
├── blocklist.py
├── system_utils.py
├── check_domain.py
│
├── data/
│   ├── blocklist.txt
│   ├── whitelist.txt
│   └── custom_blocklist.txt
│
├── backups/
│   └── .gitkeep
│
├── .gitignore
├── README.md
└── requirements.txt
```

Your actual `.bak` backup files should NOT appear on GitHub.

---

# Part 2 - Push Your Project to Your Personal Repository

If your project folder is not already connected to GitHub, create a new repository on your GitHub account.

Do not initialize the GitHub repository with extra files if you already created your files locally.

Copy the repository URL.

It will look similar to:

```text
https://github.com/YOUR-USERNAME/tb-ad-blocker.git
```

Open the terminal inside your project folder.

Initialize Git:

```bash
git init
```

Add your files:

```bash
git add .
```

Create your first commit:

```bash
git commit -m "Complete TB Ad Blocker project"
```

Connect your GitHub repository:

```bash
git remote add origin https://github.com/YOUR-USERNAME/tb-ad-blocker.git
```

Make sure your branch is named `main`:

```bash
git branch -M main
```

Push your project:

```bash
git push -u origin main
```

Open your repository on GitHub and confirm that your files appear.

---

# Part 3 - Check Your Personal Repository

Before continuing, check your GitHub repository.

You should NOT see files such as:

```text
hosts_original.bak
hosts_20261020_184500.bak
```

If you accidentally uploaded a personal backup file, remove it before submitting your project.

You should also make sure your README explains:

- What your project does
- How the ad blocker works
- Features you completed
- Technologies used
- How to run the program
- Safety features
- Known limitations
- Optional features you added
- What you learned

---

# Part 4 - Fork the Trailblazers Repository

Now you will submit your project to the Trailblazers Software Projects repository.

Go to:

**TB-Software-Projects**

On the top-right side of the repository page, click:

```text
Fork
```

GitHub will ask where you want to create the fork.

Choose your own GitHub account.

You can keep the repository name:

```text
TB-Software-Projects
```

Click:

```text
Create fork
```

GitHub will create your own copy of the Trailblazers repository.

Your fork will look similar to:

```text
github.com/YOUR-USERNAME/TB-Software-Projects
```

The original Trailblazers repository belongs to the Software Team.

Your fork is your own copy where you are allowed to make changes.

---

# Part 5 - Clone Your Fork

Open your fork:

```text
github.com/YOUR-USERNAME/TB-Software-Projects
```

Click the green:

```text
Code
```

button.

Copy the HTTPS URL.

It should look similar to:

```text
https://github.com/YOUR-USERNAME/TB-Software-Projects.git
```

Open a terminal in the location where you want to keep the repository.

Run:

```bash
git clone https://github.com/YOUR-USERNAME/TB-Software-Projects.git
```

Then enter the repository:

```bash
cd TB-Software-Projects
```

---

# Part 6 - Create Your Submission Branch

Do NOT make your project submission directly on the `main` branch.

Create your own branch.

Use this naming format:

```text
firstname-lastname-project1
```

Example:

```bash
git checkout -b maya-smith-project1
```

Replace `maya-smith` with your own name.

Check your branch:

```bash
git branch
```

The branch with the `*` beside it is your current branch.

---

# Part 7 - Find the Project Submission Folder

Inside the Trailblazers repository, navigate to:

```text
Fall 2026/
└── Project 1 - Ad Blocker/
    └── Submissions/
```

Inside `Submissions`, create a new folder using your name.

Use this format:

```text
First-Last
```

Example:

```text
Maya-Smith
```

Your submission should eventually look similar to:

```text
Fall 2026/
└── Project 1 - Ad Blocker/
    └── Submissions/
        └── Maya-Smith/
```

Do not put your files directly inside the main `Submissions` folder.

Every member should have their own folder.

---

# Part 8 - Add Your Project Files

Copy the safe files from your completed personal project into your submission folder.

Your submission folder should look similar to:

```text
Maya-Smith/
│
├── main.py
├── blocker.py
├── blocklist.py
├── system_utils.py
├── check_domain.py
│
├── data/
│   ├── blocklist.txt
│   ├── whitelist.txt
│   └── custom_blocklist.txt
│
├── .gitignore
├── README.md
└── requirements.txt
```

Do NOT copy your personal backup files.

Do NOT include:

```text
backups/hosts_original.bak
backups/hosts_*.bak
__pycache__/
.vscode/
```

If you include the `backups` folder at all, it should contain only:

```text
.gitkeep
```

---

# Part 9 - Check Your Data Files

Before submitting, open:

```text
data/whitelist.txt
```

and:

```text
data/custom_blocklist.txt
```

Remove anything personal that you do not want included in a public repository.

You may leave these files with comments or safe example entries.

Your main blocklist may remain in the project.

---

# Part 10 - Update Your Submission README

Your submission folder should contain a `README.md`.

This README should include a link to your personal GitHub repository.

At minimum, include:

```markdown
# TB Ad Blocker

**Member:** Your Name

## Overview

Briefly describe your version of the project.

## Features

List the major features you completed.

## Technologies

List the technologies you used.

## Personal Project Repository

[View My Full Project on GitHub](PASTE-YOUR-LINK-HERE)

## Optional Features

List any additional features you completed beyond the required project.

If you did not complete any optional features, write:

None.
```

Do not claim features that you did not personally complete and understand.

---

# Part 11 - Review Your Changes

Before committing anything, run:

```bash
git status
```

Look carefully at every file listed.

Make sure you are only adding files inside your own submission folder.

You should NOT be modifying:

```text
Project 1 - Ad Blocker/README.md
Project 1 - Ad Blocker/TUTORIAL.md
other students' submission folders
the root repository README
```

If you accidentally changed another file, fix it before continuing.

---

# Part 12 - Add Your Submission to Git

Once everything looks correct:

```bash
git add .
```

Check again:

```bash
git status
```

Make sure no backup files appear.

---

# Part 13 - Commit Your Submission

Create a commit.

Use a clear commit message such as:

```bash
git commit -m "Add Maya Smith Project 1 submission"
```

Replace the name with your own.

---

# Part 14 - Push Your Branch

Push your branch to your fork.

Example:

```bash
git push -u origin maya-smith-project1
```

Use the name of the branch you created earlier.

---

# Part 15 - Create a Pull Request

Open your fork on GitHub:

```text
github.com/YOUR-USERNAME/TB-Software-Projects
```

GitHub may display a message saying:

```text
Compare & pull request
```

Click it.

If you do not see that button:

1. Click **Pull requests**
2. Click **New pull request**
3. Choose your project submission branch

---

# Part 16 - Check the Pull Request Direction

Before submitting, make sure the pull request is going:

```text
YOUR FORK / your-project-branch
                ↓
Trailblazers TB-Software-Projects / main
```

The **base repository** should be the original Trailblazers Software Projects repository.

The **base branch** should be:

```text
main
```

The **compare branch** should be your submission branch.

---

# Part 17 - Name Your Pull Request

Use this title format:

```text
Project 1 - Your Name
```

Example:

```text
Project 1 - Maya Smith
```

---

# Part 18 - Complete the Pull Request Description

Use the pull request template provided by the repository.

Before submitting, confirm:

- Your project works
- Your personal repository is public
- Your personal repository has a completed README
- Your Trailblazers submission is inside your own folder
- Your personal repository link works
- You did not include personal backup files
- You understand the code you submitted

Add any additional notes if necessary.

---

# Part 19 - Submit the Pull Request

Click:

```text
Create pull request
```

Your submission is now waiting for review.

Do NOT merge your own pull request into the Trailblazers repository.

The Software Director will review the submission.

You may be asked to make changes before it is accepted.

---

# If Changes Are Requested

Do NOT create a new pull request.

Make the requested changes in the same local branch.

Then run:

```bash
git add .
```

Commit the changes:

```bash
git commit -m "Address Project 1 review feedback"
```

Push again:

```bash
git push
```

Your existing pull request will update automatically.

---

# Browser-Only Submission Option

If you are unable to use the Git command line, you may submit through GitHub's website.

You still need to fork the Trailblazers repository first.

## Step 1

Fork:

```text
TB-Software-Projects
```

to your GitHub account.

## Step 2

Open your fork.

Navigate to:

```text
Fall 2026/
Project 1 - Ad Blocker/
Submissions/
```

## Step 3

Create your personal submission folder.

Use:

```text
First-Last/
```

## Step 4

Upload your safe project files into that folder.

Do NOT upload:

```text
hosts_original.bak
hosts_*.bak
__pycache__/
.vscode/
```

## Step 5

Commit the uploaded files to a new branch.

Do not submit directly to the original Trailblazers `main` branch.

## Step 6

Open a pull request from your fork back to:

```text
TB-Software-Projects → main
```

Use:

```text
Project 1 - Your Name
```

as the pull request title.

---

# Submission Checklist

Before opening your pull request, confirm:

- [ ] My project works.
- [ ] My project is pushed to my personal GitHub repository.
- [ ] My personal repository is public.
- [ ] My personal repository has a completed README.
- [ ] My Trailblazers submission is inside my own folder.
- [ ] My submission includes my source code.
- [ ] My submission README links to my personal repository.
- [ ] I did not submit any personal hosts-file backups.
- [ ] I did not modify another member's submission.
- [ ] I did not modify the Trailblazers project instructions.
- [ ] I tested my project before submitting it.
- [ ] I can explain the code I submitted.

---

# Need Help?

If you run into problems with:

- Forking
- Cloning
- Branches
- Git commands
- Push errors
- Pull requests
- Merge conflicts
- Project submission structure

Ask in the Trailblazers Software Team GroupMe or bring the issue to a Software Team meeting.

Do not wait until the submission deadline to ask for help.
