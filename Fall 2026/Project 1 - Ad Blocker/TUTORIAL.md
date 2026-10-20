# TB Ad Blocker - Build Tutorial

In this project, you will build a real system-wide ad blocker using Python.

You will NOT be given the completed program.

Instead, this tutorial gives you:

- The files you need
- The functions you need to create
- Part of the code structure
- Instructions inside the code
- Blanks for you to complete
- Hints for each section
- Tests so you can check your work as you go

The goal is to help you build the program yourself without having to guess what you are supposed to do.

---

# Table of Contents

1. Understanding the Project
2. Project Setup
3. Understanding the Hosts File
4. Creating the Blocklist
5. Reading and Processing Domains
6. Backing Up the Hosts File
7. Building the Ad Blocker
8. Enabling and Disabling Blocking
9. Whitelist and Custom Blocklist
10. Building the Main Menu
11. Testing the Program
12. Running With Administrator Permissions
13. GitHub and Documentation
14. Troubleshooting
15. Optional Extensions

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

Instead of reaching the real advertising server, the request gets sent to an address that leads nowhere.

The advertisement or tracker cannot load normally.

---

## Important Limitation

This type of ad blocker blocks **domains**.

It cannot:

- Block one individual element on a webpage
- Block an ad that comes from the exact same domain as the content you want
- Automatically block every subdomain
- Guarantee that every application will use the computer's normal hosts-file lookup

So this is a real ad blocker, but it will not block every possible advertisement.

---

## Before Moving On

Make sure you can explain:

1. What is a domain?
2. What is an IP address?
3. What does DNS do?
4. What does the hosts file do?
5. Why would pointing an ad domain to `0.0.0.0` prevent it from loading?
6. Why can't this program block every ad?

---

# Part 2: Project Setup

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

## Step 2.2: Create Your Project

Create a folder named:

```text
tb-ad-blocker
```

Open that folder in VS Code.

---

## Step 2.3: Create the Files

Create this structure:

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

### What each Python file does

**`main.py`**

The menu and everything the user interacts with.

**`blocker.py`**

The main blocking logic.

**`blocklist.py`**

Loads, cleans, adds, removes, and manages domains.

**`system_utils.py`**

Handles the operating system, hosts file, backups, administrator permissions, and DNS cache.

**`check_domain.py`**

A small testing program used to check whether a domain is currently resolving.

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

### Why?

Your backup files contain a copy of the hosts file from **your own computer**.

Those files should never be uploaded to GitHub.

---

## Step 3.2: `requirements.txt`

This project uses Python's standard library.

Open:

```text
requirements.txt
```

Add a comment explaining that there are no external packages required.

### Hint

A Python comment begins with:

```python
#
```

---

# Part 4: Create the Starter Blocklists

## Step 4.1: Main Blocklist

Open:

```text
data/blocklist.txt
```

Add:

```text
# TB Ad Blocker - Starter Blocklist

example.com
ads.example.com
tracker.example.com
```

We are starting with a tiny list for testing.

---

## Step 4.2: Whitelist

Open:

```text
data/whitelist.txt
```

Add:

```text
# Domains in this file should NEVER be blocked.
```

---

## Step 4.3: Custom Blocklist

Open:

```text
data/custom_blocklist.txt
```

Add:

```text
# Add your own extra blocked domains here.
```

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

Research or inspect the output of:

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
        # Build this path:
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

Verify that the path looks correct for your computer.

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

# Part 8: Build `blocklist.py`

Now we will work with the domain files.

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

from datetime import datetime
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

Look up:

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

A blocklist may contain several formats:

```text
example.com
```

or:

```text
0.0.0.0 example.com
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

So:

```python
parts[0]
```

is the first item.

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

### Why a Set?

A set:

- Automatically removes duplicates
- Makes checking whether something exists fast

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

Do not just say:

```text
Permission denied
```

Explain what happened and what the user should do.

---

# Part 19: Safely Write the Hosts File

This is one of the most important parts of the project.

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

Do NOT intentionally break your real hosts file.

Test this function using a fake hosts file first.

Your test should prove:

1. A normal write works.
2. A failed write causes the backup to be restored.
3. The broken content does not remain.

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

Anything outside these markers must stay untouched.

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

### Why does the order matter?

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

### Main Rule

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

This function should **build** the result in memory first.

It should not modify the real file.

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


    # Do not continue with an empty list.
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


    # TODO: Display the detected operating system.


    # TODO: Display the hosts-file path.


    # TODO: Display whether the program currently has
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

# Part 33: Whitelist and Custom Blocklist

Return to:

```text
main.py
```

But first, make sure `blocklist.py` has:

```python
def add_domain_to_file(path, domain):
    # Completed earlier
    pass


def remove_domain_from_file(path, domain):
    # Completed earlier
    pass
```

These same functions will work for:

- Whitelist
- Custom blocklist

You do not need separate versions for each list.

---

# Part 34: Optional Online Blocklist Updates

Return to:

```text
blocklist.py
```

Create a constant for the online blocklist source:

```python
BLOCKLIST_URL = '____________________________________________'
```

Your instructor will provide or approve the blocklist source.

Then create:

```python
def download_blocklist(url=BLOCKLIST_URL):
    """
    Download an updated public blocklist.

    Return:
        (True, success_message)

    or:
        (False, error_message)
    """

    # TODO:
    # Create an HTTP request using urllib.request.


    try:

        # TODO:
        # Open the URL with a timeout.


        # TODO:
        # Read and decode the downloaded text.


    except (OSError, ValueError) as error:

        return False, f'Download failed: {error}'


    # TODO:
    # Create an empty set for new domains.


    # TODO:
    # Process every downloaded line using
    # extract_domain_from_line().


    # SAFETY:
    # If fewer than 10 valid domains were downloaded,
    # DO NOT replace the existing blocklist.


    # TODO:
    # If an existing blocklist exists,
    # make a .bak copy first.


    # TODO:
    # Save the new domains.


    # TODO:
    # Return True and a helpful success message.
```

This feature is not needed to understand basic ad blocking, but it allows the application to refresh its domain list later.

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
            # is rebuilt with the updated lists.
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


    # If invalid:
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
    2. Download a fresh blocklist
    3. Cancel
    """

    print()
    print('--- Update / Reload Blocklist ---')

    print('1. Reload current list files')
    print('2. Download a fresh blocklist')
    print('3. Cancel')


    # TODO:
    # Ask the user for a choice.
    choice = ______________________________


    if choice == '1':

        # TODO:
        # Count the current domains to block.


        # TODO:
        # Print the count.


        # TODO:
        # Offer to apply the changes.
        pass


    elif choice == '2':

        # TODO:
        # Ask the user to confirm the download.


        # TODO:
        # Call download_blocklist().


        # TODO:
        # Display the returned message.


        # TODO:
        # If successful, offer to apply the changes.
        pass


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
    # explain that the OS is unsupported and stop.


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
            # Update/reload blocklist.
            ______________________________


        elif choice == '9':

            # TODO:
            # Restore original hosts file.
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

Use harmless test domains first.

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

It should NOT appear in the final set returned by:

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

Confirm that:

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

Your program should STOP instead of guessing what to delete.

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

---

# Part 46: Test Real Blocking

Start with a harmless test domain.

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

# Part 47: Test Whitelisting

1. Add a domain to the blocklist.
2. Add the same domain to the whitelist.
3. Enable blocking.
4. Inspect the hosts file.

The whitelisted domain should not appear in the TB blocker section.

---

# Part 48: Test the Custom Blocklist

1. Add a new domain through the menu.
2. Apply the change.
3. Inspect the hosts file.
4. Confirm the domain appears.

---

# Part 49: Test Restore

Before testing Restore Original:

Make sure you understand that this is different from **Disable Blocking**.

### Disable Blocking

Removes only the TB Ad Blocker section.

### Restore Original

Replaces the entire hosts file with the permanent original backup.

When testing restore:

1. Confirm an original backup exists.
2. Confirm the program warns you.
3. Confirm it asks for explicit confirmation.
4. Confirm it makes a backup of the current file first.
5. Confirm the original file is restored.

---

# Part 50: GitHub

Your project should be stored in your own personal GitHub repository.

Suggested name:

```text
tb-ad-blocker
```

Before committing:

```bash
git status
```

Make sure files such as:

```text
hosts_original.bak
hosts_20261020_184500.bak
```

are NOT listed as files that will be committed.

---

## Basic Git Workflow

```bash
git add .
git commit -m "Describe what you changed"
git push
```

Do not wait until the entire project is finished to make one giant commit.

Make commits as you complete meaningful parts of the project.

---

# Part 51: Personal README

Your personal repository should include your own `README.md`.

Include:

- Project title
- What the application does
- How it works
- Features you completed
- Technologies used
- Project structure
- How to run it
- Safety features
- Known limitations
- Screenshots or demo
- Any optional features you added
- What you learned

Do not claim you completed a feature that you did not implement.

---

# Part 52: Troubleshooting

## `python` is not recognized

Make sure Python is installed.

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

## Permission Denied

The hosts file requires elevated permission.

### Windows

Restart PowerShell/Terminal using:

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

This is because malware can also misuse the hosts file.

Make sure:

- You are running your own project
- You understand the changes being made
- Your backup exists

Do not disable security software simply to make the project work.

---

## Blocking Is Enabled But the Website Still Loads

Possible reasons:

- DNS information is cached
- The browser is still open
- The domain being blocked is not actually the domain serving the ad
- The browser/application may use its own DNS system
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

Do not keep running Enable/Disable repeatedly.

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

Inspect the hosts file carefully.

You should normally have exactly:

```text
# === TB AD BLOCKER START ===
```

and:

```text
# === TB AD BLOCKER END ===
```

---

## Blocklist Download Fails

The core blocker should still work with the local blocklist.

Check:

- Internet connection
- Blocklist URL
- Firewall/network restrictions

Do not erase a working local list because a download failed.

---

# Part 53: Optional Extensions

Complete the core project before starting these.

Possible extensions include:

- Tkinter graphical interface
- Automatic blocklist updates
- Multiple blocklist sources
- Blocklist statistics
- Search blocked domains
- Logging
- Analytics dashboard
- Scheduled updates
- System tray controls
- Start automatically when the computer starts
- Local DNS filtering
- Socket programming
- DNS request logging
- DNS caching

---

# Final Check

Before considering your project complete, make sure you can explain:

1. What is DNS?
2. What is a hosts file?
3. What does `0.0.0.0` do in this project?
4. Why are administrator permissions required?
5. What is a set?
6. Why did we use a set for domains?
7. What does the whitelist do?
8. What does the custom blocklist do?
9. What happens when blocking is enabled?
10. What happens when blocking is disabled?
11. Why are START and END markers used?
12. Why do we create backups?
13. What is the difference between the original backup and timestamped backups?
14. Why do we verify the hosts file after writing?
15. What happens if writing fails?
16. What does `try/except` do?
17. What does a `for` loop do?
18. What is a function?
19. Why can't this project block every advertisement?
20. What is the difference between disabling blocking and restoring the original hosts file?
21. Why might a browser still load something after the hosts file changes?
22. Why should personal backup files never be pushed to GitHub?
23. What part of your project was most difficult?
24. What would you improve if you had more time?

If you used AI or outside resources while building the project, you should still be able to answer these questions in your own words.
