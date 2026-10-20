# TB Ad Blocker - Build Tutorial

In this project, you will build a real system-wide ad blocker using Python.

You will **NOT** be given the completed program.

Instead, this tutorial gives you:

- The files you need
- The functions you need to create
- Part of the code structure
- Instructions inside the code
- Blanks for you to complete
- Hints for each section
- Tests so you can check your work as you go

The goal is to help you build the program yourself without having to guess what you are supposed to do.

You will write and test your code in **Visual Studio Code**, but your project will be connected to **GitHub from the beginning**.

---

# Project Roadmap

You will:

1. Create your personal project repository on GitHub
2. Clone it into VS Code
3. Learn how DNS and the hosts file work
4. Create and process domain lists
5. Build hosts-file backups
6. Build the blocking system
7. Add whitelist and custom blocklist support
8. Download the real public ad/tracker blocklist
9. Build the command-line menu
10. Test everything safely
11. Complete your personal GitHub repository and documentation

---

# Part 1: Understanding the Project

Before writing code, make sure you understand what the program is actually doing.

## What is a domain?

A domain is the name we normally use to visit a website.

Examples:

```text
google.com
github.com
example.com
```

Computers communicate using numerical addresses called **IP addresses**, so the computer has to figure out which IP address belongs to a domain.

---

## What is DNS?

DNS stands for **Domain Name System**.

You can think of DNS like the internet's phone book.

You know:

```text
example.com
```

Your computer needs something more like:

```text
93.184.216.34
```

DNS helps your computer translate the domain name into an IP address.

---

## What is the hosts file?

Your computer also has a local file called the **hosts file**.

The hosts file can manually tell your computer which address should be used for a domain.

A line could look like:

```text
127.0.0.1 localhost
```

For this project, our program will eventually add entries like:

```text
0.0.0.0 ads.example.com
```

Instead of reaching the real advertising server, the request is redirected away from that server.

The advertisement or tracker cannot load normally.

---

## Important Limitation

This type of ad blocker blocks **domains**.

It cannot:

- Block one individual element on a webpage
- Block an ad that comes from the exact same domain as the content you want
- Automatically block every subdomain
- Guarantee that every application will use the computer's normal hosts-file lookup

For example:

```text
example.com
```

and:

```text
ads.example.com
```

are different hostnames.

Blocking one does not automatically block the other.

This is a real ad-blocking technique, but it will not block every possible advertisement.

---

## Before Moving On

Make sure you can explain:

1. What is a domain?
2. What is an IP address?
3. What does DNS do?
4. What does the hosts file do?
5. Why can changing a hosts-file entry stop a domain from loading normally?
6. Why can't this program block every ad?

---

# Part 2: Create Your Project on GitHub

For this project, you will create your personal GitHub repository **before** creating the project files.

Your workflow will be:

```text
GitHub Repository
        ↓
Clone Repository
        ↓
VS Code
        ↓
Write + Test Code
        ↓
Commit
        ↓
Push Back to GitHub
```

Your code will still be written and tested in VS Code.

GitHub will store the online version of your project.

---

## Step 2.1: Check Python

Open a terminal.

### Windows

```bash
python --version
```

If that does not work:

```bash
py --version
```

### macOS/Linux

```bash
python3 --version
```

You should have Python 3.8 or newer.

---

## Step 2.2: Check Git

Run:

```bash
git --version
```

You should see a Git version number.

If Git is not installed, install Git before continuing.

---

## Step 2.3: Create Your Personal GitHub Repository

Go to GitHub and sign into your account.

Click:

```text
New repository
```

Use this repository name:

```text
tb-ad-blocker
```

Set the repository to:

```text
Public
```

Check:

```text
Add a README file
```

Then click:

```text
Create repository
```

You should now have a personal repository named:

```text
tb-ad-blocker
```

This is the repository you will eventually be able to use on your resume and portfolio.

---

## Step 2.4: Clone Your Repository Into VS Code

**Cloning** creates a copy of your GitHub repository on your computer and keeps it connected to GitHub.

Open VS Code.

### Windows

Press:

```text
Ctrl + Shift + P
```

### macOS

Press:

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

Go back to your `tb-ad-blocker` repository on GitHub.

Click:

```text
Code
```

Make sure:

```text
HTTPS
```

is selected.

Copy the repository link.

Paste it into VS Code.

Choose where you want the repository saved on your computer.

When VS Code asks whether you want to open the cloned repository, choose:

```text
Open
```

---

## Step 2.5: Confirm the Repository Was Cloned

In the VS Code Explorer, you should see:

```text
tb-ad-blocker/
└── README.md
```

The folder you are looking at in VS Code is your local copy of the same project that exists on GitHub.

---

## Step 2.6: Create the Project Files

Inside the cloned `tb-ad-blocker` repository, create:

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

Your `README.md` already exists because GitHub created it.

Do not create a second README.

---

## What Each Python File Does

### `main.py`

Handles the menu and everything the user interacts with.

### `blocker.py`

Contains the main ad-blocking logic.

### `blocklist.py`

Loads, cleans, adds, removes, downloads, and manages domains.

### `system_utils.py`

Handles:

- Operating-system detection
- Hosts-file location
- Administrator permissions
- Backups
- Safe file writing
- DNS cache flushing

### `check_domain.py`

A small testing program used to check where a domain currently resolves.

---

## Step 2.7: Make Your First Commit

Save all your files.

Open the VS Code terminal.

Run:

```bash
git status
```

You should see the new files you created.

Add them:

```bash
git add .
```

Create a commit:

```bash
git commit -m "Set up ad blocker project structure"
```

Push it to GitHub:

```bash
git push
```

Refresh your repository on GitHub.

Your project structure should now appear there.

---

## Git Vocabulary

### Repository

A project that Git keeps track of.

### Clone

Create a local copy of a GitHub repository.

### Commit

A saved checkpoint of your work.

### Push

Send your local commits to GitHub.

### Pull

Bring newer changes from GitHub onto your computer.

You will use this process throughout the project:

```text
Write Code
    ↓
Test It
    ↓
git add .
    ↓
git commit
    ↓
git push
```

Do not wait until the entire project is finished before making another commit.

---

# Part 3: Protect Your Personal Files

## Step 3.1: `.gitignore`

Open:

```text
.gitignore
```

Add:

```text
__pycache__/
*.pyc
.DS_Store
.vscode/
scratch.py

# Personal hosts-file backups
backups/*.bak

# Old blocklist saved during updates
data/blocklist.txt.bak
```

---

## Why?

Your backup files contain a copy of the hosts file from **your own computer**.

Those files should never be uploaded to GitHub.

A `.gitignore` tells Git:

```text
Do not track these files.
```

---

## Step 3.2: `requirements.txt`

This project uses only Python's standard library.

That means students do not need to install extra Python packages.

Open:

```text
requirements.txt
```

Add a comment explaining that no external packages are required.

### Hint

A Python comment begins with:

```python
#
```

---

# Part 4: Understand the Blocklists

The final project will use a **real public list of advertising and tracking domains**.

You do **not** need to research, collect, or create your own main ad blocklist.

This project uses:

```text
Peter Lowe's Ad and Tracking Server List
```

The program will use this hosts-format blocklist:

```text
https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0
```

Later, your Python program will download this list automatically.

Before using thousands of real domains, however, you will use a tiny test list.

This makes it much easier and safer to tell whether your code is working.

---

## Step 4.1: Understand the Three Domain Files

Your project has:

```text
data/blocklist.txt
data/whitelist.txt
data/custom_blocklist.txt
```

### `blocklist.txt`

The main list of advertising and tracking domains.

At first, it will contain only safe test domains.

Later, your program will replace those test domains with the real Peter Lowe blocklist.

### `whitelist.txt`

Domains that should **never** be blocked.

If a domain appears in both the blocklist and whitelist:

```text
whitelist wins
```

### `custom_blocklist.txt`

Extra domains that the user personally wants to block.

These are added in addition to the public blocklist.

---

## Step 4.2: Create the Safe Test Blocklist

Open:

```text
data/blocklist.txt
```

Add:

```text
# TB Ad Blocker - Safe Test Blocklist
# This file will later be replaced with the real public blocklist.

example.com
ads.example.com
tracker.example.com
```

These are development/testing entries.

They are **not** your final real ad blocklist.

---

## Step 4.3: Whitelist

Open:

```text
data/whitelist.txt
```

Add:

```text
# TB Ad Blocker - Whitelist
# Domains in this file should NEVER be blocked.
```

Leave the rest empty for now.

---

## Step 4.4: Custom Blocklist

Open:

```text
data/custom_blocklist.txt
```

Add:

```text
# TB Ad Blocker - Custom Blocklist
# Additional domains the user personally wants blocked.
```

Leave the rest empty for now.

---

## Final Blocklist Logic

Eventually your program will calculate:

```text
Peter Lowe Blocklist
        +
Custom Blocklist
        -
Whitelist
        =
Final Domains to Block
```

You will write the Python that performs this logic later.

---

# Part 5: Build `system_utils.py`

This file handles things related to the user's computer.

---

## Step 5.1: Imports and Paths

Open:

```text
system_utils.py
```

Start with:

```python
# system_utils.py
# Functions in this file interact with the operating system.

import ctypes
import os
import platform
import shutil
import subprocess

from datetime import datetime
from pathlib import Path


# TODO: Create a variable called BASE_DIR.
# It should represent the folder containing this Python file.
BASE_DIR = ______________________________


# TODO: Create BACKUP_DIR.
# It should point to a folder named "backups" inside BASE_DIR.
BACKUP_DIR = ______________________________


# TODO: Create ORIGINAL_BACKUP_PATH.
# It should point to "hosts_original.bak" inside the backups folder.
ORIGINAL_BACKUP_PATH = ______________________________
```

### Fill-in Hints

- `Path(__file__)` refers to the current Python file.
- `.resolve()` gets its full location.
- `.parent` gets the folder containing it.
- You can combine `Path` objects using `/`.

---

## Step 5.2: Detect the Operating System

Create:

```python
def get_os_name():
    """
    Return:
        'windows'
        'macos'
        'linux'
        or 'unknown'
    """

    # TODO: Use platform.system() to find the operating system.
    system_name = __________________


    # TODO:
    # If system_name is "Windows", return "windows".
    if __________________:
        return __________________


    # TODO:
    # Apple computers return "Darwin".
    elif __________________:
        return __________________


    # TODO:
    # Linux returns "Linux".
    elif __________________:
        return __________________


    # If none match, return "unknown".
    else:
        return __________________
```

### Fill-in Hints

Inspect:

```python
platform.system()
```

Remember that capitalization matters.

---

## Step 5.3: Test It

Create a temporary file:

```text
scratch.py
```

Add:

```python
import system_utils

print(system_utils.get_os_name())
```

Run:

```bash
python scratch.py
```

or:

```bash
python3 scratch.py
```

You should see:

```text
windows
```

or:

```text
macos
```

or:

```text
linux
```

---

# Part 6: Find the Hosts File

Return to:

```text
system_utils.py
```

Create:

```python
def get_hosts_path():
    """
    Return the location of the hosts file as a Path object.
    """

    # TODO: Get the operating system using get_os_name().
    os_name = __________________


    if os_name == 'windows':

        # TODO:
        # Get the Windows SystemRoot environment variable.
        # If it cannot be found, use C:/Windows as the default.
        system_root = os.environ.get(__________________, __________________)

        # TODO:
        # Build:
        #
        # System32/drivers/etc/hosts
        #
        return Path(system_root) / _______ / _______ / _______ / _______


    elif os_name == 'macos' or os_name == 'linux':

        # TODO:
        # macOS and Linux use:
        #
        # /etc/hosts
        #
        return Path(__________________)


    else:

        # TODO:
        # Raise a RuntimeError explaining that this OS is unsupported.
        raise __________________
```

### Fill-in Hints

Windows hosts file:

```text
C:\Windows\System32\drivers\etc\hosts
```

macOS/Linux:

```text
/etc/hosts
```

---

## Test It

In `scratch.py`:

```python
import system_utils

print(system_utils.get_hosts_path())
```

Verify that the location looks correct for your computer.

---

# Part 7: Read a Text File

Still inside `system_utils.py`, create:

```python
def read_text_file(path):
    """
    Read an entire text file and return its contents as one string.
    """

    # TODO:
    # Open path in READ mode using UTF-8.
    with open(path, '_____', encoding='utf-8') as file:

        # TODO:
        # Read the entire file and return it.
        return file.________()
```

### Fill-in Hints

File modes:

```text
r = read
w = write
a = append
```

Which one do you want here?

---

## Test the Real Hosts File Safely

Reading the hosts file does **not** modify it.

In `scratch.py`:

```python
import system_utils

hosts_path = system_utils.get_hosts_path()

print(system_utils.read_text_file(hosts_path))
```

You should see the contents of your computer's hosts file.

Do not edit it yet.

---

## Git Checkpoint

After Parts 5 through 7 work:

```bash
git add .
git commit -m "Add operating system and hosts file utilities"
git push
```

---

# Part 8: Build `blocklist.py`

Open:

```text
blocklist.py
```

---

## Step 8.1: Imports and File Paths

Start with:

```python
# blocklist.py
# Functions in this file manage domain lists.

import shutil
import urllib.request

from pathlib import Path


# TODO: Create BASE_DIR just like you did in system_utils.py.
BASE_DIR = ______________________________


# TODO: Create DATA_DIR.
# It should point to the "data" folder.
DATA_DIR = ______________________________


# TODO: Create paths for each data file.

BLOCKLIST_FILE = ______________________________

WHITELIST_FILE = ______________________________

CUSTOM_BLOCKLIST_FILE = ______________________________


# This is the real public ad/tracker list used by this project.
# You do NOT need to find your own list.
BLOCKLIST_URL = 'https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0'
```

### Fill-in Hints

The three filenames are:

```text
blocklist.txt
whitelist.txt
custom_blocklist.txt
```

---

## Step 8.2: Domain Rules

Add:

```python
# Characters that are allowed inside a normal domain label.
ALLOWED_CHARACTERS = 'abcdefghijklmnopqrstuvwxyz0123456789-_'

# Public hosts lists may begin lines with either of these.
HOSTS_FILE_ADDRESSES = ('0.0.0.0', '127.0.0.1')

# Domains that our program should never intentionally block.
NEVER_BLOCK_DOMAINS = {'localhost.localdomain'}
```

Peter Lowe's downloaded list uses hosts-file lines such as:

```text
127.0.0.1 advertising-domain.com
```

Our program only needs the domain:

```text
advertising-domain.com
```

Later, our own blocker will build entries using:

```text
0.0.0.0
```

---

# Part 9: Read Lines From a File

Create:

```python
def read_lines(path):
    """
    Return all lines in a file as a list.

    If the file does not exist, return an empty list.
    """

    try:

        # TODO:
        # Open the file in read mode.
        with open(path, '_____', encoding='utf-8', errors='replace') as file:

            # TODO:
            # Read the file and split it into separate lines.
            return file.________().________()

    except FileNotFoundError:

        # TODO:
        # Return an empty list.
        return ________
```

### Fill-in Hints

An empty list is:

```python
[]
```

Research:

```text
Python splitlines
```

---

# Part 10: Validate a Domain

Create:

```python
def is_valid_domain(domain):
    """
    Return True if domain looks valid.
    Return False otherwise.
    """

    # TODO:
    # Reject domains longer than 253 characters.
    # Also reject text with no "." in it.
    if __________________ or __________________:
        return False


    # TODO:
    # Split the domain anywhere there is a period.
    labels = domain.________('.')


    # Check every piece of the domain.
    for label in labels:

        # TODO:
        # Reject an empty label.
        # Reject labels longer than 63 characters.
        if __________________:
            return False


        # TODO:
        # Reject labels that begin OR end with "-".
        if __________________ or __________________:
            return False


        # Check each character.
        for character in label:

            # TODO:
            # If the character is NOT in ALLOWED_CHARACTERS,
            # return False.
            if __________________:
                return False


    # TODO:
    # If the final section is completely numeric,
    # it may be an IP address instead of a domain.
    if __________________:
        return False


    # If we reached this point, the domain passed every test.
    return ________
```

### Fill-in Hints

Useful methods:

```text
.split()
.startswith()
.endswith()
.isdigit()
```

Remember:

```python
labels[-1]
```

means the last item in a list.

---

## Test It

Try:

```python
import blocklist

tests = [
    'example.com',
    'ads.example.com',
    'localhost',
    'not a domain!',
    '0.0.0.0',
    '-bad.example.com'
]

for domain in tests:
    print(domain, blocklist.is_valid_domain(domain))
```

Decide which values should return `True` and which should return `False`.

---

# Part 11: Extract a Domain From a Line

A blocklist may contain:

```text
example.com
```

or:

```text
0.0.0.0 example.com
```

or:

```text
127.0.0.1 example.com
```

or:

```text
example.com # comment
```

Create:

```python
def extract_domain_from_line(line):
    """
    Get a clean domain from one line.

    Return the domain if valid.
    Return None if the line should be ignored.
    """

    # TODO:
    # Remove anything after a # comment.
    line = line.________('#')[0]


    # TODO:
    # Remove extra spaces and convert to lowercase.
    line = line.________().________()


    # If nothing remains, ignore the line.
    if line == '':
        return None


    # TODO:
    # Split the remaining text by whitespace.
    parts = line.________()


    # If there is only one item,
    # treat it as the possible domain.
    if len(parts) == 1:
        candidate = __________________


    # If the line begins with a recognized hosts-file address,
    # use the second item as the domain.
    elif len(parts) >= 2 and parts[0] in HOSTS_FILE_ADDRESSES:
        candidate = __________________


    else:
        return None


    # TODO:
    # Use is_valid_domain() to check candidate.
    if __________________:
        return __________________


    return None
```

### Fill-in Hints

Lists start counting at `0`.

```python
parts[0]
```

is the first item.

```python
parts[1]
```

is the second.

---

# Part 12: Turn a File Into a Set of Domains

Create:

```python
def read_domains_from_file(path):
    """
    Read a file and return all valid domains as a set.
    """

    # TODO:
    # Create an empty set.
    domains = ________()


    # TODO:
    # Loop through every line returned by read_lines(path).
    for line in __________________:

        # TODO:
        # Extract a domain from the current line.
        domain = __________________


        # If a valid domain was found:
        if domain is not None:

            # TODO:
            # Add it to the set.
            domains.________(domain)


    return domains
```

---

## Why a Set?

A set:

- Automatically removes duplicates
- Makes checking whether something already exists fast

---

## Create the Loader Functions

```python
def load_blocklist_domains():
    # TODO:
    # Return the domains inside BLOCKLIST_FILE.
    return ______________________________


def load_whitelist_domains():
    # TODO:
    # Return the domains inside WHITELIST_FILE.
    return ______________________________


def load_custom_domains():
    # TODO:
    # Return the domains inside CUSTOM_BLOCKLIST_FILE.
    return ______________________________
```

---

# Part 13: Determine Which Domains Should Actually Be Blocked

Create:

```python
def get_domains_to_block():
    """
    Return the final set of domains that should be blocked.
    """

    # TODO:
    # Load the normal blocklist.
    blocked = ______________________________


    # TODO:
    # Combine it with the custom blocklist.
    blocked = blocked | ______________________________


    # TODO:
    # Load the whitelist.
    allowed = ______________________________


    # TODO:
    # Return:
    #
    # blocked domains
    # MINUS whitelisted domains
    # MINUS NEVER_BLOCK_DOMAINS
    #
    return ______________________________
```

### Fill-in Hints

For Python sets:

```text
| combines sets
- removes one set from another
```

---

# Part 14: Save List Files

Create:

```python
def write_lines(path, lines):
    """
    Write a collection of lines to a file.
    """

    # TODO:
    # Make sure DATA_DIR exists.
    DATA_DIR.mkdir(exist_ok=________)


    # TODO:
    # Open path in WRITE mode.
    with open(path, '_____', encoding='utf-8') as file:

        for line in lines:

            # TODO:
            # Write the line followed by a newline.
            file.write(______________________________)
```

---

# Part 15: Clean a Domain Typed by the User

A user may type:

```text
google.com
```

or:

```text
https://google.com
```

or:

```text
https://google.com/page
```

Create:

```python
def clean_user_domain(user_text):
    """
    Clean a domain entered by the user.
    """

    # TODO:
    # Remove surrounding spaces and convert to lowercase.
    text = user_text.________().________()


    # Remove http:// or https:// if either appears.
    for prefix in ('https://', 'http://'):

        if text.startswith(prefix):

            # TODO:
            # Remove the prefix from the beginning.
            text = ______________________________


    # TODO:
    # Remove anything after the first "/".
    text = ______________________________


    # TODO:
    # Remove a port number such as :8080 if present.
    text = ______________________________


    # TODO:
    # Validate the final result.
    if __________________:
        return text


    return None
```

---

# Part 16: Add and Remove Domains

Create:

```python
def add_domain_to_file(path, domain):
    """
    Add a domain to a file.

    Return True if added.
    Return False if it already existed.
    """

    # TODO:
    # Check whether domain is already in the file.
    if __________________:
        return False


    # TODO:
    # Read the current lines.
    lines = __________________


    # TODO:
    # Add domain to the list.
    lines.________(domain)


    # TODO:
    # Save the updated lines.
    ______________________________


    return True
```

Now create:

```python
def remove_domain_from_file(path, domain):
    """
    Remove a domain from a file.

    Return True if removed.
    Return False if not found.
    """

    kept_lines = []
    removed = False


    # TODO:
    # Loop through every existing line.
    for line in __________________:


        # TODO:
        # If this line contains the domain we want to remove:
        if __________________:

            removed = True


        else:

            # TODO:
            # Keep the line.
            ______________________________


    if removed:

        # TODO:
        # Rewrite the file using kept_lines.
        ______________________________


    return removed
```

---

## Git Checkpoint

Once your list processing works:

```bash
git add .
git commit -m "Add blocklist processing"
git push
```

---

# Part 17: Back Up the Hosts File

Return to:

```text
system_utils.py
```

Create:

```python
def backup_hosts_file():
    """
    Create:
    1. One permanent original backup
    2. One timestamped backup every time
    """

    # TODO:
    # Get the hosts-file path.
    hosts_path = __________________


    # TODO:
    # Create the backups folder if necessary.
    BACKUP_DIR.________(exist_ok=________)


    # Only create the original backup once.
    if not ORIGINAL_BACKUP_PATH.________():

        # TODO:
        # Copy the hosts file to ORIGINAL_BACKUP_PATH.
        shutil.________(hosts_path, ORIGINAL_BACKUP_PATH)


    # TODO:
    # Get the current date/time.
    # Format it so it can safely be used in a filename.
    timestamp = datetime.now().strftime(__________________)


    # TODO:
    # Create a filename similar to:
    #
    # hosts_20261020_184500.bak
    #
    backup_path = ______________________________


    # TODO:
    # Copy the current hosts file to backup_path.
    ______________________________


    return backup_path
```

### Fill-in Hints

Look up:

```text
shutil.copy2
Path.exists
datetime strftime
```

Suggested timestamp information:

```text
year month day hour minute second
```

---

# Part 18: Check Administrator Permissions

Add to `system_utils.py`:

```python
def is_admin():
    """
    Return True if running as administrator/root.
    Return False otherwise.
    """

    try:

        if get_os_name() == 'windows':

            # TODO:
            # Use ctypes to ask Windows if this program
            # is running as Administrator.
            return ______________________________


        # macOS/Linux:
        # Root has an effective user ID of 0.
        return ______________________________


    except (AttributeError, OSError):

        # If something unexpected happens,
        # use the SAFE answer.
        return ________
```

### Fill-in Hints

Research:

```text
ctypes IsUserAnAdmin Python
os.geteuid Python
```

---

## Explain the Permission Requirement

Create:

```python
def explain_admin_requirement():
    """
    Explain why elevated permission is required
    and tell the user how to restart the program.
    """

    os_name = get_os_name()


    print()
    print('This action needs administrator/root permission.')


    # TODO:
    # Print an explanation telling the user WHY
    # the hosts file is protected.


    if os_name == 'windows':

        # TODO:
        # Tell the user to reopen PowerShell/Terminal
        # using "Run as administrator".
        pass


    elif os_name == 'macos' or os_name == 'linux':

        # TODO:
        # Tell the user they can run:
        #
        # sudo python3 main.py
        #
        pass
```

Do not only print:

```text
Permission denied
```

The program should explain what happened and what the user should do.

---

# Part 19: Safely Write the Hosts File

This is one of the most important parts of the entire project.

Create:

```python
def write_hosts_file_safely(new_text, backup_path):
    """
    Write new_text to the hosts file.

    If something goes wrong after writing begins,
    restore backup_path.
    """

    # TODO:
    # Find the real hosts file.
    hosts_path = __________________


    # Track whether writing actually started.
    write_started = False


    try:

        # TODO:
        # Open the hosts file in write mode.
        with open(hosts_path, '_____', encoding='utf-8') as file:

            # The file is now being modified.
            write_started = ________


            # TODO:
            # Write new_text.
            ______________________________


            # TODO:
            # Flush Python's file buffer.
            ______________________________


            # TODO:
            # Ask the operating system to flush the file to disk.
            ______________________________


        # TODO:
        # Read the hosts file back.
        # Compare it to new_text.
        #
        # If they do NOT match, raise an OSError.
        if ______________________________:
            raise OSError('Hosts-file verification failed.')


    except Exception:

        # Only restore if writing actually began.
        if write_started:

            try:

                # TODO:
                # Restore the backup to the hosts-file location.
                ______________________________


            except OSError:

                print('WARNING: Automatic restore failed.')
                print('Restore this backup manually:', backup_path)


        # TODO:
        # Re-raise the ORIGINAL error.
        ________
```

### Fill-in Hints

Useful tools:

```text
file.write()
file.flush()
os.fsync()
file.fileno()
shutil.copyfile()
raise
```

---

## Important Test

Do **not** intentionally break your real hosts file.

Test this function using a fake file first.

Your test should prove:

1. A normal write works.
2. A failed write causes the backup to be restored.
3. Broken content does not remain.

---

# Part 20: Flush the DNS Cache

Create:

```python
def run_command(command_parts):
    """
    Run an operating-system command.

    Return True if successful.
    Return False otherwise.
    """

    try:

        # TODO:
        # Run command_parts using subprocess.
        # Capture the output.
        # Use text mode.
        # Add a timeout.
        result = subprocess.________(
            command_parts,
            capture_output=________,
            text=________,
            timeout=20
        )


        # A successful terminal command normally returns code 0.
        return result.returncode == ________


    except (OSError, subprocess.TimeoutExpired):

        return False
```

Now create:

```python
def flush_dns():
    """
    Flush the DNS cache for the current operating system.
    """

    os_name = get_os_name()
    success = False


    if os_name == 'windows':

        # TODO:
        # Run:
        #
        # ipconfig /flushdns
        #
        success = ______________________________


    elif os_name == 'macos':

        # TODO:
        # Run BOTH:
        #
        # dscacheutil -flushcache
        # killall -HUP mDNSResponder
        #
        first_worked = ______________________________
        second_worked = ______________________________

        success = ______________________________


    elif os_name == 'linux':

        linux_commands = [
            ['resolvectl', 'flush-caches'],
            ['systemd-resolve', '--flush-caches'],
            ['nscd', '-i', 'hosts'],
        ]


        # TODO:
        # Try each command.
        # If one works:
        # - set success to True
        # - stop the loop
        for command in linux_commands:

            if __________________:
                __________________
                __________________


    if success:
        print('DNS cache flushed.')

    else:
        print('Could not automatically flush the DNS cache.')
        print('Try reopening your browser or restarting your computer.')


    return success
```

---

## Git Checkpoint

```bash
git add .
git commit -m "Add hosts file backup and safety utilities"
git push
```

---

# Part 21: Start `blocker.py`

Open:

```text
blocker.py
```

Start with:

```python
# blocker.py
# Main ad-blocking logic.

import blocklist
import system_utils


MARKER_START = '# === TB AD BLOCKER START ==='

MARKER_END = '# === TB AD BLOCKER END ==='

BLOCK_ADDRESS = '0.0.0.0'
```

These markers tell the program:

```text
THIS part belongs to us.
```

Anything outside those markers must remain untouched.

---

# Part 22: Check Permission Before Changing Anything

Create:

```python
def check_admin_or_explain():
    """
    Return True if the program can modify the hosts file.

    If not, explain why and return False.
    """

    # TODO:
    # Ask system_utils whether the program has admin rights.
    if __________________:

        return True


    # TODO:
    # Display the administrator explanation.
    ______________________________


    return False
```

---

# Part 23: Friendly Error Messages

Create:

```python
def print_friendly_error(error):
    """
    Convert common Python errors into messages
    a beginner can understand.
    """

    # TODO:
    # Handle PermissionError.
    if isinstance(error, __________________):

        print('Permission denied.')
        print('Make sure you started the program as administrator/root.')


    # TODO:
    # Handle FileNotFoundError.
    elif isinstance(error, __________________):

        print('A needed file could not be found.')


    # TODO:
    # Handle UnicodeDecodeError BEFORE ValueError.
    elif isinstance(error, __________________):

        print('The hosts file contains text this program could not read safely.')


    # TODO:
    # Handle ValueError.
    elif isinstance(error, __________________):

        print('Safety check stopped the operation.')


    else:

        print('Unexpected problem:', error)


    print('Backups are stored in:', system_utils.BACKUP_DIR)
```

---

## Why Does the Order Matter?

Some Python exceptions are more specific versions of other exceptions.

Handle the more specific error first.

---

# Part 24: Remove the Old Blocker Section

Create:

```python
def remove_blocker_section(hosts_text):
    """
    Return hosts_text WITHOUT the TB Ad Blocker section.

    Do NOT remove anything else.
    """

    kept_lines = []

    inside_section = False


    # TODO:
    # Loop through every line.
    for line in hosts_text.________():

        stripped_line = line.strip()


        # START marker found.
        if stripped_line == MARKER_START:

            # TODO:
            # If we were already inside a section,
            # something is wrong with the markers.
            if inside_section:
                raise ______________________________


            inside_section = ________


        # END marker found.
        elif stripped_line == MARKER_END:

            # TODO:
            # If we were NOT inside a section,
            # the markers are damaged.
            if not inside_section:
                raise ______________________________


            inside_section = ________


        # If inside our section:
        elif inside_section:

            # TODO:
            # Do NOT save this line.
            ________


        else:

            # TODO:
            # Preserve this unrelated line.
            ______________________________


    # TODO:
    # If the file ended while inside the section,
    # the END marker was missing.
    if __________________:
        raise ______________________________


    # TODO:
    # Rebuild the remaining lines into one string
    # and return it.
    return ______________________________
```

---

## Main Rule

Anything outside:

```text
# === TB AD BLOCKER START ===
```

and:

```text
# === TB AD BLOCKER END ===
```

must survive.

---

# Part 25: Build the Blocker Section

Create:

```python
def build_blocker_section(domains):
    """
    Create our marked section of the hosts file.
    """

    # Start with the marker.
    lines = [
        MARKER_START,
        '# Managed by TB Ad Blocker. Do not edit between these markers.'
    ]


    # TODO:
    # Sort domains and loop through each one.
    for domain in __________________:


        # TODO:
        # Add a line containing:
        #
        # BLOCK_ADDRESS + domain
        #
        # Example:
        # 0.0.0.0 ads.example.com
        #
        lines.________(__________________)


    # TODO:
    # Add MARKER_END.
    ______________________________


    # TODO:
    # Join the lines with newline characters.
    return ______________________________
```

---

# Part 26: Build the Complete New Hosts Text

Create:

```python
def build_hosts_text_with_blocking(current_hosts_text, domains):
    """
    Return what the hosts file SHOULD look like
    when blocking is enabled.

    Do not write anything here.
    """

    # TODO:
    # Remove an old TB section if one exists.
    clean_text = ______________________________


    # TODO:
    # Build a fresh blocker section.
    blocker_section = ______________________________


    # TODO:
    # Combine the preserved hosts text
    # with the new blocker section.
    return ______________________________
```

This function should **build** the new file in memory first.

It should not modify the real hosts file.

---

# Part 27: Detect Whether Blocking Is Enabled

Create:

```python
def has_blocker_section(hosts_text):
    """
    Return True if MARKER_START exists in the hosts text.
    """

    # TODO:
    # Look through every line.
    for line in __________________:

        if __________________:
            return True


    return False
```

---

## Count Blocked Domains

Create:

```python
def count_blocked_domains_in_hosts(hosts_text):
    """
    Count blocking entries between the markers.
    """

    count = 0
    inside_section = False


    for line in hosts_text.splitlines():

        stripped_line = line.strip()


        # TODO:
        # Turn inside_section on when START is found.


        # TODO:
        # Turn inside_section off when END is found.


        # TODO:
        # While inside the section,
        # count lines beginning with BLOCK_ADDRESS.


    return count
```

---

# Part 28: Enable Blocking

Create:

```python
def enable_blocking():
    """
    Turn blocking on.

    Return True if successful.
    Return False otherwise.
    """

    print()
    print('--- Enable Ad Blocking ---')


    # TODO:
    # Check administrator permission.
    # Stop if permission is missing.
    if not __________________:
        return False


    # TODO:
    # Get the final domains to block.
    domains = ______________________________


    if len(domains) == 0:

        print('There are no domains to block.')

        return False


    try:

        # TODO:
        # Get the hosts-file path.
        hosts_path = ______________________________


        # TODO:
        # Read the current hosts-file text.
        current_text = ______________________________


        # TODO:
        # Build the NEW hosts text.
        new_text = ______________________________


        # TODO:
        # Back up the hosts file BEFORE changing it.
        backup_path = ______________________________


        # TODO:
        # Safely write new_text.
        ______________________________


    except (OSError, ValueError, RuntimeError) as error:

        # TODO:
        # Display a friendly error.
        ______________________________

        return False


    print('Blocking is now ENABLED.')


    # TODO:
    # Flush DNS.
    ______________________________


    return True
```

---

# Part 29: Disable Blocking

Create:

```python
def disable_blocking():
    """
    Turn blocking off without deleting unrelated hosts entries.
    """

    print()
    print('--- Disable Ad Blocking ---')


    # TODO:
    # Check administrator rights.
    if not __________________:
        return False


    try:

        # TODO:
        # Get the hosts-file path.


        # TODO:
        # Read the hosts file.


        # TODO:
        # If our section does not exist,
        # explain that blocking is already off.


        # TODO:
        # Remove ONLY our section.


        # TODO:
        # Create a backup BEFORE writing.


        # TODO:
        # Safely save the cleaned hosts text.


    except (OSError, ValueError, RuntimeError) as error:

        # TODO:
        # Print a friendly error.

        return False


    print('Blocking is now DISABLED.')


    # TODO:
    # Flush DNS.


    return True
```

---

# Part 30: Determine Current Blocking Status

Create:

```python
def is_blocking_enabled():
    """
    Return True if blocking is currently enabled.
    """

    try:

        # TODO:
        # Read the real hosts file.
        hosts_text = ______________________________


    except (OSError, ValueError, RuntimeError):

        return False


    # TODO:
    # Return whether our section exists.
    return ______________________________
```

---

# Part 31: Show Status

Create:

```python
def show_status():
    """
    Display information about the current blocker.
    """

    print()
    print('--- Blocking Status ---')


    # TODO:
    # Display the detected operating system.


    # TODO:
    # Display the hosts-file path.


    # TODO:
    # Display whether the program currently has
    # administrator/root permission.


    # TODO:
    # Read the hosts file safely.


    # TODO:
    # If our section exists:
    # - print ENABLED
    # - count how many domains are currently in it


    # Otherwise:
    # - print DISABLED


    # TODO:
    # Print:
    # - number of main blocklist domains
    # - number of custom domains
    # - number of whitelist domains


    # TODO:
    # Tell the user whether the permanent original backup exists.
```

---

# Part 32: Restore the Original Hosts File

Create:

```python
def restore_original_hosts():
    """
    Restore hosts_original.bak.

    WARNING:
    This replaces the entire current hosts file.
    """

    print()
    print('--- Restore Original Hosts File ---')


    # TODO:
    # Check administrator rights.


    # TODO:
    # Check whether ORIGINAL_BACKUP_PATH exists.
    # If it does not exist, stop.


    print('WARNING: This will replace the ENTIRE current hosts file.')


    # TODO:
    # Ask the user to type YES exactly.


    # TODO:
    # If they do not type YES, cancel.


    try:

        # TODO:
        # Read the original backup.


        # TODO:
        # Back up the CURRENT hosts file first.


        # TODO:
        # Safely write the original text.


    except (OSError, ValueError, RuntimeError) as error:

        # TODO:
        # Display friendly error.

        return False


    # TODO:
    # Flush DNS.


    return True
```

---

## Git Checkpoint

```bash
git add .
git commit -m "Build core ad blocking logic"
git push
```

---

# Part 33: Whitelist and Custom Blocklist

The same functions you already created will be used for both lists:

```python
def add_domain_to_file(path, domain):
    # You already created this earlier.
    pass


def remove_domain_from_file(path, domain):
    # You already created this earlier.
    pass
```

You do **not** need separate functions for:

```text
whitelist
```

and:

```text
custom blocklist
```

Instead, the program passes the correct file path into the same reusable function.

---

# Part 34: Download the Real Ad/Tracker Blocklist

You have been using a tiny test list while building the program.

Now you will create the feature that downloads the **real blocklist**.

The blocklist source is already provided.

You do not need to find your own.

Your `BLOCKLIST_URL` should already be:

```python
BLOCKLIST_URL = 'https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0'
```

When a download succeeds, the real domains will replace the temporary test entries inside:

```text
data/blocklist.txt
```

---

## Step 34.1: Create `download_blocklist()`

Inside:

```text
blocklist.py
```

create:

```python
def download_blocklist(url=BLOCKLIST_URL):
    """
    Download the real public ad/tracker blocklist.

    Return:
        (True, success_message)

    or:
        (False, error_message)
    """

    # TODO:
    # Create an HTTP request.
    #
    # Use urllib.request.Request().
    # Give it a User-Agent such as:
    #
    # TB-Ad-Blocker/1.0
    #
    request = urllib.request.________(
        url,
        headers={
            'User-Agent': 'TB-Ad-Blocker/1.0'
        }
    )


    try:

        # TODO:
        # Open the request.
        # Use a timeout of 20 seconds.
        with urllib.request.________(request, timeout=20) as response:


            # TODO:
            # Read the downloaded bytes.
            # Decode them into UTF-8 text.
            downloaded_text = ______________________________


    except (OSError, ValueError) as error:

        return False, f'Download failed: {error}'


    # TODO:
    # Create an empty SET for valid downloaded domains.
    new_domains = ________()


    # TODO:
    # Split downloaded_text into lines.
    # Loop through each line.
    for line in __________________:


        # TODO:
        # Use extract_domain_from_line().
        domain = ______________________________


        if domain is not None:

            # TODO:
            # Add the domain to new_domains.
            ______________________________


    # SAFETY:
    #
    # A real blocklist should contain many valid domains.
    #
    # If fewer than 10 valid domains were received,
    # assume the download is broken.
    #
    # DO NOT replace the current working blocklist.
    if len(new_domains) < 10:

        return False, 'The download did not contain enough valid domains. The existing blocklist was kept.'


    # TODO:
    # If BLOCKLIST_FILE already exists:
    #
    # copy it to:
    #
    # data/blocklist.txt.bak
    #
    if BLOCKLIST_FILE.________():

        ______________________________


    # TODO:
    # Sort the downloaded domains.
    # Save them into BLOCKLIST_FILE.
    ______________________________


    return True, f'Saved {len(new_domains)} domains to the blocklist.'
```

### Fill-in Hints

Useful tools:

```text
urllib.request.Request
urllib.request.urlopen
response.read()
.decode()
.splitlines()
set()
.add()
Path.exists()
shutil.copy2()
sorted()
write_lines()
```

---

## What Happened to the Test Blocklist?

At the beginning, `blocklist.txt` contained:

```text
example.com
ads.example.com
tracker.example.com
```

Those were only there to help you build and test the program safely.

After a successful real blocklist download:

```text
data/blocklist.txt
```

will contain the actual public ad/tracker domains.

You are **not** expected to manually type thousands of domains.

---

## Important Safety Rule

Never replace a working blocklist with an empty or obviously broken download.

That is why your program checks the number of valid domains **before** replacing the file.

---

# Part 35: Build `main.py`

Open:

```text
main.py
```

Start with:

```python
# main.py
# User interface for TB Ad Blocker.

import blocker
import blocklist
import system_utils


MENU_TEXT = """
==============================
         TB Ad Blocker
==============================
 1. Enable Ad Blocking
 2. Disable Ad Blocking
 3. View Blocking Status
 4. Add Domain to Whitelist
 5. Remove Domain from Whitelist
 6. Add Custom Domain to Blocklist
 7. Remove Custom Domain
 8. Update/Reload Blocklist
 9. Restore Original Hosts File
10. Exit
==============================
"""
```

---

# Part 36: Welcome Message

Create:

```python
def show_welcome():
    """
    Display basic information when the application starts.
    """

    print('TB Ad Blocker')


    # TODO:
    # Explain that this program blocks whole domains
    # and cannot block every possible ad.


    # TODO:
    # Display the operating system.


    # TODO:
    # Display the hosts-file path.


    # TODO:
    # Display whether the program currently has
    # administrator permissions.
```

---

# Part 37: Yes/No Questions

Create:

```python
def ask_yes_no(question):
    """
    Keep asking until the user enters yes or no.

    Return True for yes.
    Return False for no.
    """

    while True:

        # TODO:
        # Ask the question and clean the response.
        answer = ______________________________


        # TODO:
        # Accept "y" and "yes".
        if __________________:
            return True


        # TODO:
        # Accept "n" and "no".
        elif __________________:
            return False


        print('Please type y or n.')
```

---

# Part 38: Apply List Changes

Create:

```python
def offer_to_apply_changes():
    """
    If blocking is already ON, ask whether the user
    wants to apply their list change immediately.
    """

    # TODO:
    # Check whether blocking is enabled.
    if __________________:


        # TODO:
        # Ask whether the user wants to apply changes now.
        if __________________:


            # TODO:
            # Re-enable blocking so the hosts file
            # is rebuilt using the updated lists.
            ______________________________


    else:

        print('The change will be used the next time blocking is enabled.')
```

---

# Part 39: Add a Domain From the Menu

Create:

```python
def add_domain_flow(file_path, list_name):
    """
    Ask the user for a domain and add it to file_path.
    """

    # TODO:
    # Ask the user for a domain.
    text = ______________________________


    # TODO:
    # Clean the input.
    domain = ______________________________


    if domain is None:

        print('That does not look like a valid domain.')

        return


    # TODO:
    # Try adding it to the file.
    if __________________:

        print(f'Added {domain} to the {list_name}.')

        # TODO:
        # Offer to apply the change immediately.
        ______________________________


    else:

        print(f'{domain} is already in the {list_name}.')
```

---

# Part 40: Remove a Domain From the Menu

Create:

```python
def remove_domain_flow(file_path, list_name):
    """
    Ask the user for a domain and remove it.
    """

    # TODO:
    # Ask for the domain.


    # TODO:
    # Clean the domain.


    # TODO:
    # Reject invalid input.


    # TODO:
    # Attempt to remove the domain.


    # If removed:
    # - tell the user
    # - offer to apply changes


    # If not found:
    # - tell the user
```

---

# Part 41: Update or Reload the Blocklist

Create:

```python
def handle_update_blocklist():
    """
    Allow the user to:

    1. Reload current list files
    2. Download the real public blocklist
    3. Cancel
    """

    print()
    print('--- Update / Reload Blocklist ---')

    print('1. Reload current list files')
    print('2. Download the latest Peter Lowe blocklist')
    print('3. Cancel')


    # TODO:
    # Ask the user for a choice.
    choice = ______________________________


    if choice == '1':

        # TODO:
        # Count the current domains to block.
        count = ______________________________


        # TODO:
        # Print the count.


        # TODO:
        # Offer to apply the changes.
        ______________________________


    elif choice == '2':

        print('This will download the public ad/tracker blocklist.')
        print('Your old blocklist will be backed up first.')


        # TODO:
        # Ask whether the user wants to continue.
        if not __________________:

            print('Cancelled.')
            return


        # TODO:
        # Call download_blocklist().
        success, message = ______________________________


        # TODO:
        # Display the returned message.
        print(__________________)


        # TODO:
        # If download succeeded,
        # offer to apply the updated list.
        if __________________:

            ______________________________


    else:

        print('Cancelled.')
```

---

# Part 42: Main Menu Loop

Create:

```python
def main():
    """
    Run the TB Ad Blocker menu.
    """

    # TODO:
    # If get_os_name() returns "unknown",
    # explain that the operating system is unsupported
    # and stop the program.


    # TODO:
    # Show the welcome message.


    while True:

        print(MENU_TEXT)


        # TODO:
        # Ask the user for a menu option.
        choice = ______________________________


        if choice == '1':

            # TODO:
            # Enable blocking.
            ______________________________


        elif choice == '2':

            # TODO:
            # Disable blocking.
            ______________________________


        elif choice == '3':

            # TODO:
            # Show status.
            ______________________________


        elif choice == '4':

            # TODO:
            # Add a domain to WHITELIST_FILE.
            ______________________________


        elif choice == '5':

            # TODO:
            # Remove a domain from WHITELIST_FILE.
            ______________________________


        elif choice == '6':

            # TODO:
            # Add a domain to CUSTOM_BLOCKLIST_FILE.
            ______________________________


        elif choice == '7':

            # TODO:
            # Remove a domain from CUSTOM_BLOCKLIST_FILE.
            ______________________________


        elif choice == '8':

            # TODO:
            # Update/reload the blocklist.
            ______________________________


        elif choice == '9':

            # TODO:
            # Restore the original hosts file.
            ______________________________


        elif choice == '10':

            print('Goodbye!')

            # TODO:
            # Exit the while loop.
            ________


        else:

            print('Please enter a number from 1 to 10.')


        input('\nPress Enter to return to the menu...')
```

At the bottom:

```python
if __name__ == '__main__':

    try:

        # TODO:
        # Start main().
        ______________________________


    except (KeyboardInterrupt, EOFError):

        print('\nExiting. Goodbye!')
```

---

## Git Checkpoint

```bash
git add .
git commit -m "Add command line menu and blocklist download"
git push
```

---

# Part 43: Create `check_domain.py`

Open:

```text
check_domain.py
```

Start with:

```python
# check_domain.py
# Test where a domain currently resolves.

import socket


# TODO:
# Ask the user for a domain.
domain = ______________________________


try:

    # TODO:
    # Use socket.gethostbyname() to resolve the domain.
    address = socket.__________________(domain)


    print(f'{domain} resolves to {address}')


    # TODO:
    # If address is 0.0.0.0,
    # tell the user the domain appears to be blocked.
    if __________________:

        print('This domain appears to be BLOCKED.')


except socket.gaierror:

    print('The domain could not be resolved.')
```

Do not use `nslookup` or `dig` as your main hosts-file test.

Those tools may query DNS directly and can give confusing results for this project.

---

# Part 44: Test the Program Safely

Do not start by blocking random important websites.

Use the small test list first.

---

## Test 1: Operating System

Run:

```text
get_os_name()
```

Confirm that the correct operating system is detected.

---

## Test 2: Hosts Path

Run:

```text
get_hosts_path()
```

Confirm that the correct hosts-file location appears.

---

## Test 3: Read-Only Hosts File

Use:

```text
read_text_file()
```

Confirm that you can read the hosts file without changing anything.

---

## Test 4: Domain Processing

Test:

```text
example.com
ADS.EXAMPLE.COM
https://example.com
not a domain
0.0.0.0
```

Make sure invalid entries are rejected.

---

## Test 5: Sets and Duplicates

Place the same domain in the blocklist twice.

Make sure the final domain set contains it only once.

---

## Test 6: Whitelist

Place the same domain in:

```text
blocklist.txt
```

and:

```text
whitelist.txt
```

It should **not** appear in the final set returned by:

```text
get_domains_to_block()
```

---

## Test 7: Backup

Run the backup function.

Confirm:

- `hosts_original.bak` is created the first time
- A timestamped backup is also created
- The original backup is not replaced on later runs

---

## Test 8: Safe Writing

Use a **fake hosts file** first.

Prove that:

- A normal write works
- A simulated failed write restores the backup

Do not intentionally cause the real hosts file to fail.

---

## Test 9: Build Blocker Text

Use fake hosts text.

Confirm:

- Existing lines stay
- The START marker is added
- Domains appear between the markers
- The END marker is added

---

## Test 10: Remove Blocker Text

Confirm:

- Only the TB Ad Blocker section disappears
- Existing hosts entries remain

---

## Test 11: Damaged Markers

Test fake text containing:

- START with no END
- END with no START
- Two START markers

Your program should **STOP** instead of guessing what to delete.

---

## Test 12: Blocklist Download

Run your blocklist download feature.

Confirm:

1. The download succeeds.
2. `data/blocklist.txt` now contains many real domains.
3. Your previous test list was backed up as:

```text
data/blocklist.txt.bak
```

4. Invalid/comment lines from the downloaded source are ignored.
5. `get_domains_to_block()` still returns a set of valid domains.

Do not manually type the real blocklist.

Your program should download and process it.

---

# Part 45: Run the Real Blocker

Only do this after all earlier tests pass.

---

## Windows

Open PowerShell or Windows Terminal using:

```text
Run as administrator
```

Navigate to your project folder.

Run:

```bash
python main.py
```

or:

```bash
py main.py
```

---

## macOS/Linux

Navigate to your project folder.

Run:

```bash
sudo python3 main.py
```

Your password may not appear while you type.

That is normal.

---

# Part 46: Test Real Blocking

Start with a harmless test domain before relying on the full real blocklist.

Before blocking:

```bash
python check_domain.py
```

Check its normal result.

Then:

1. Enable blocking.
2. Run `check_domain.py` again.
3. Confirm the domain no longer resolves normally or resolves to the blocking address.
4. Disable blocking.
5. Test again.
6. Confirm normal behavior returns.

Also inspect the hosts file and verify that only the TB section changed.

---

# Part 47: Test the Real Blocklist

Once your safe testing is successful:

1. Use menu option 8.
2. Download the real public blocklist.
3. Confirm thousands of valid domains were loaded.
4. Enable blocking.
5. Check your status screen.
6. Confirm the hosts file contains the TB markers and downloaded blocked domains.

Do not manually paste the entire public blocklist into your hosts file.

Your program should handle it.

---

# Part 48: Test Whitelisting

1. Choose a domain currently in the blocklist.
2. Add the same domain to the whitelist.
3. Apply the changes.
4. Inspect the hosts file.

The whitelisted domain should **not** appear in the TB blocker section.

---

# Part 49: Test the Custom Blocklist

1. Add a safe test domain through the menu.
2. Apply the change.
3. Inspect the hosts file.
4. Confirm the domain appears.

---

# Part 50: Test Restore

Before testing Restore Original, understand that it is different from **Disable Blocking**.

## Disable Blocking

Removes only:

```text
# === TB AD BLOCKER START ===
...
# === TB AD BLOCKER END ===
```

Everything else remains.

## Restore Original

Replaces the entire current hosts file with the permanent original backup.

When testing restore:

1. Confirm an original backup exists.
2. Confirm the program warns you.
3. Confirm it asks for explicit confirmation.
4. Confirm it makes a backup of the current file first.
5. Confirm the original file is restored.

---

# Part 51: Keep GitHub Updated

Your personal repository was created at the beginning of the project.

Now make sure your finished code is actually pushed to it.

Run:

```bash
git status
```

Review every file listed.

Files such as these should **NOT** be committed:

```text
backups/hosts_original.bak
backups/hosts_20261020_184500.bak
data/blocklist.txt.bak
__pycache__/
.vscode/
scratch.py
```

---

## Final Project Commit

When your project is working:

```bash
git add .
```

Then:

```bash
git status
```

Read the list before committing.

If everything is correct:

```bash
git commit -m "Complete TB Ad Blocker project"
```

Then:

```bash
git push
```

Refresh GitHub.

Make sure your current project files are visible online.

---

## Good Git Habits

Do not make only one commit for the entire project.

Your history should show progress.

Examples:

```text
Set up ad blocker project structure
Add hosts file utilities
Add blocklist processing
Add hosts file backup and safety utilities
Build core ad blocking logic
Add command line menu and blocklist download
Complete project testing and documentation
```

You do not need to use those exact messages.

Your messages should clearly describe what changed.

---

# Part 52: Personal README

Your personal repository already has a `README.md`.

Now update it so it describes **your finished project**.

Do not simply copy the Trailblazers assignment README.

Your README should include:

- Project title
- What the application does
- How the blocker works
- Features you completed
- Technologies used
- Project structure
- How to run the program
- How to use the menu
- Safety features
- Known limitations
- Screenshots or demo
- Optional features you added
- What you learned

If you did not build an optional feature, do not claim that you did.

---

# Part 53: Trailblazers Submission

After your personal repository is complete:

1. Make sure your personal repository is public.
2. Make sure your finished code is pushed.
3. Make sure your README is complete.
4. Make sure no personal backup files are on GitHub.
5. Follow the Trailblazers Project 2 submission instructions.

The Trailblazers submission process will have you:

```text
Fork the TB-Software-Projects repository
        ↓
Clone your fork
        ↓
Create your own submission branch
        ↓
Add your project to your personal submission folder
        ↓
Push your branch
        ↓
Open a Pull Request
```

Use the full instructions here:

```text
Project 2 - Ad Blocker/Submissions/README.md
```

Do not submit personal hosts-file backups to the Trailblazers repository.

---

# Part 54: Troubleshooting

## `python` Is Not Recognized

Try:

```bash
python --version
```

or:

```bash
py --version
```

On macOS/Linux:

```bash
python3 --version
```

---

## `git` Is Not Recognized

Run:

```bash
git --version
```

If Git is not installed, install Git and restart VS Code.

---

## Git Push Fails

First run:

```bash
git status
```

Then check:

```bash
git remote -v
```

Make sure your project is connected to your own:

```text
tb-ad-blocker
```

repository.

If GitHub asks you to authenticate, complete the GitHub sign-in process.

---

## Permission Denied

The hosts file requires elevated permission.

### Windows

Restart PowerShell or Windows Terminal using:

```text
Run as administrator
```

### macOS/Linux

Use:

```bash
sudo python3 main.py
```

---

## Windows Security Warns About the Hosts File

Windows Security may warn when a program modifies the hosts file.

That can happen because harmful software can also misuse the hosts file.

Make sure:

- You are running your own project
- You understand what the program is changing
- Your backup exists

Do **not** disable your computer's security software simply to make the project work.

If a managed or protected computer prevents the change, do not try to bypass that protection.

---

## Blocking Is Enabled but the Website Still Loads

Possible reasons:

- DNS information is cached
- The browser is still open
- The domain being blocked is not actually the domain serving the ad
- The browser or application may use its own DNS system
- DNS-over-HTTPS, a VPN, or a proxy may bypass normal host resolution
- The site may use a different subdomain

Try:

1. Flush DNS.
2. Completely close and reopen the browser.
3. Check the exact domain using `check_domain.py`.
4. Confirm the domain appears between your hosts-file markers.

Remember:

```text
example.com
```

and:

```text
www.example.com
```

are different exact hostnames.

---

## My Hosts File Looks Wrong

Stop making changes.

Do not keep running Enable and Disable repeatedly.

Check:

```text
backups/
```

Your program should contain:

```text
hosts_original.bak
```

and timestamped safety backups.

Use the restore feature only after understanding which backup you are restoring.

---

## Broken START/END Markers

If your program reports damaged markers, do not have the program guess which lines belong to it.

You should normally have exactly one:

```text
# === TB AD BLOCKER START ===
```

and one:

```text
# === TB AD BLOCKER END ===
```

The program should stop if the markers are damaged rather than risk deleting unrelated entries.

---

## Blocklist Download Fails

The program should keep the existing blocklist.

Check:

- Internet connection
- The blocklist URL
- Firewall or network restrictions

Do not erase a working list because a download failed.

The URL being used by this project is stored in:

```python
BLOCKLIST_URL
```

Do not replace it with random blocklists from the internet.

---

## `blocklist.txt` Still Has Only Three Domains

If you still see:

```text
example.com
ads.example.com
tracker.example.com
```

you are still using the development test list.

Use the program's **Update/Reload Blocklist** option to download the real list.

---

# Part 55: Optional Extensions

Complete the required project first.

Then you may add additional features.

Possible extensions include:

- Tkinter graphical interface
- Scheduled automatic blocklist updates
- Multiple trusted blocklist sources
- Blocklist statistics
- Search blocked domains
- Logging
- Analytics dashboard
- System tray controls
- Start automatically when the computer starts
- Local DNS filtering
- Socket programming
- DNS request logging
- DNS caching

These are optional.

The normal ability to **download the provided Peter Lowe blocklist through the menu is part of the project**, not an optional extension.

---

# Final Project Checklist

Before considering your project complete, confirm:

- [ ] My personal GitHub repository exists.
- [ ] I cloned my repository and worked on it in VS Code.
- [ ] My project has multiple meaningful Git commits.
- [ ] My latest code is pushed to GitHub.
- [ ] My operating system is detected correctly.
- [ ] My program finds the correct hosts file.
- [ ] My program can read the hosts file.
- [ ] My domain parser works.
- [ ] Duplicate domains are removed.
- [ ] My whitelist works.
- [ ] My custom blocklist works.
- [ ] My program downloads the provided real blocklist.
- [ ] A failed blocklist download does not destroy the existing list.
- [ ] My program creates an original hosts-file backup.
- [ ] My program creates timestamped backups.
- [ ] My personal backups are ignored by Git.
- [ ] My program detects administrator/root permissions.
- [ ] My program safely writes and verifies the hosts file.
- [ ] A failed write restores a backup.
- [ ] My program preserves unrelated hosts-file entries.
- [ ] Damaged markers cause the program to stop safely.
- [ ] I can enable blocking.
- [ ] I can disable blocking.
- [ ] I can view blocker status.
- [ ] I can restore the original hosts file.
- [ ] My DNS cache flush is handled safely.
- [ ] `check_domain.py` works.
- [ ] My personal README is complete.
- [ ] I tested the project before submitting it.

---

# Make Sure You Can Explain Your Project

Before submitting, make sure you can answer these questions in your own words:

1. What is DNS?
2. What is a hosts file?
3. What does `0.0.0.0` do in this project?
4. Why are administrator permissions required?
5. What is a set?
6. Why did we use a set for domains?
7. What does the main blocklist do?
8. Where does the real main blocklist come from?
9. Why did we use a small test list first?
10. What does the whitelist do?
11. What does the custom blocklist do?
12. How is the final set of blocked domains calculated?
13. What happens when blocking is enabled?
14. What happens when blocking is disabled?
15. Why are START and END markers used?
16. Why do we create backups?
17. What is the difference between the original backup and timestamped backups?
18. Why do we verify the hosts file after writing?
19. What happens if writing fails?
20. What does `try/except` do?
21. What does a `for` loop do?
22. What is a function?
23. Why can't this project block every advertisement?
24. What is the difference between disabling blocking and restoring the original hosts file?
25. Why might a browser still load something after the hosts file changes?
26. Why should personal backup files never be pushed to GitHub?
27. What does cloning a GitHub repository mean?
28. What is the difference between a commit and a push?
29. What part of your project was most difficult?
30. What would you improve if you had more time?

If you used AI or outside resources while building the project, you should still be able to explain every part of the code you submitted.
