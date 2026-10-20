# Project 1 - Ad Blocker

## Overview

For our first Fall 2026 project, you will build a real system-wide ad blocker using Python.

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
