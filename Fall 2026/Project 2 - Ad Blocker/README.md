# Project 2 - Ad Blocker

## Overview

For our second Fall 2026 project, you will build a real system-wide ad blocker using Python.

Instead of only hiding ads inside one browser, this program will use your computer's **hosts file** to prevent known advertising and tracking domains from loading across your system.

The finished program will allow you to turn blocking on and off, manage blocked domains, whitelist domains, view the current blocking status, and safely restore your original hosts file.

This project is designed to introduce real Python programming while also showing how software can interact with your operating system.

---

## What You Will Learn

Throughout this project, you will practice:

- Python variables and data types
- Conditionals
- Loops
- Functions
- Lists and sets
- Reading and writing files
- Imports and modules
- File paths
- Error handling with `try` and `except`
- Operating system interaction
- Git and GitHub
- Debugging and testing
- Technical documentation

You are not expected to already know all of these concepts.

We will introduce important concepts during Software Team meetings, and the project tutorial will walk through the program step by step.

---

## How the Ad Blocker Works

When your computer tries to visit a website, it has to determine the IP address associated with that domain.

Normally, your computer may use DNS to look up that address.

The **hosts file** allows your computer to manually map a domain to a specific IP address before using normal DNS resolution.

Our program will add entries such as:

```text
0.0.0.0 ads.example.com
0.0.0.0 tracker.example.com
```

`0.0.0.0` does not lead to the actual advertising server, so the connection fails and the ad or tracker cannot load normally.

Your program will manage these entries automatically.

---

## Required Features

Your completed core project must be able to:

- Enable ad blocking
- Disable ad blocking
- Read domains from a blocklist
- View whether blocking is currently enabled
- Add domains to a whitelist
- Remove domains from a whitelist
- Add custom domains to block
- Preserve existing hosts-file entries
- Detect Windows, macOS, or Linux
- Back up the hosts file before making changes
- Restore the original hosts file
- Handle common errors without crashing
- Clearly tell the user when administrator permissions are required

Your program should only modify the section of the hosts file that belongs to your ad blocker.

Example:

```text
# === TB AD BLOCKER START ===
0.0.0.0 ads.example.com
0.0.0.0 tracker.example.com
# === TB AD BLOCKER END ===
```

---

## Safety Requirements

The hosts file is an important system file, so safety is part of the project.

Your program must:

1. Back up the hosts file before changing it.
2. Preserve entries that were already in the hosts file.
3. Clearly mark the section added by the program.
4. Remove only the program's own section when blocking is disabled.
5. Provide a way to restore the original hosts file.
6. Handle failed writes safely.
7. Never upload personal hosts-file backups to GitHub.

Only test this project on a computer you are allowed to modify.

Do not use school-managed, employer-managed, or other restricted computers if you do not have permission to change system settings.

---

## Important Limitation

This project blocks **domains**, not individual advertisements.

That means it can block many ads and trackers that come from dedicated advertising domains, but it cannot block every ad on the internet.

For example, if a website serves both its normal content and advertisements from the same domain, blocking that domain would also block the content.

This is still a real ad-blocking technique, but you should understand and be able to explain its limitations.

---

## Project Structure

Your finished project will look similar to:

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
├── .gitignore
├── README.md
└── requirements.txt
```

Each file has a different responsibility.

You will build this structure gradually throughout the tutorial.

---

## Project Tutorial

The full beginner-friendly build instructions are available here:

**[View the Project Tutorial](./TUTORIAL.md)**

The tutorial builds the project one step at a time and explains:

- What you are doing
- Why you are doing it
- The Python concepts being used
- What the code does
- How to test each step
- Common errors and troubleshooting

Do not skip directly to the finished code.

The purpose of the project is not only to make the program work, but to understand how it works.

---

## Using AI

AI tools may be used to help you:

- Understand an error
- Explain a concept
- Debug code
- Ask questions
- Review your work

However, you are responsible for understanding the code you submit.

You should be able to explain:

- What your functions do
- Why you used certain data structures
- How the hosts file works
- How your program blocks domains
- Why backups are necessary
- How your program enables and disables blocking

If you cannot explain a section of your project, you should review it before submitting.

---

## Optional Extensions

Once the required project is working, you may add additional features.

Possible extensions include:

- Graphical user interface
- Automatic blocklist updates
- Blocklist statistics
- Searchable blocklist
- Scheduled updates
- System tray controls
- Start on computer startup
- Logging
- Analytics dashboard
- Local DNS filtering
- Socket programming
- DNS caching

These are optional.

Complete and understand the core project before beginning stretch features.

---

## Before You Finish

You should be able to demonstrate:

- Blocking enabled
- Blocking disabled
- A domain being blocked
- Whitelisting
- Your backup system
- Restoring the hosts file
- Your project's GitHub repository

You should also be able to explain how your project works without reading directly from your code.

---

## Submitting Your Project

Each member will keep their completed project in their own **personal GitHub repository** and will also submit their completed project files to the **Trailblazers Software Projects repository**.

Your personal repository is the version you can use for your portfolio, resume, and job applications.

Your Trailblazers submission will be added through a **fork and pull request**.

Do not include personal hosts-file backups or other ignored/generated files in your submission.

**[View Complete Submission Instructions](./Submissions/README.md)**
