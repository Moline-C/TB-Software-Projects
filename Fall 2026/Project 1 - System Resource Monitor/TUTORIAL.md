# Project 1 - System Resource Monitor: Tutorial

**Trailblazers Software Team - Fall 2026**

In this tutorial you will build the **TB System Resource Monitor**, a command-line Python program that shows how your computer's CPU, memory (RAM), and disk are being used, warns you when something is running high, lists the programs using the most memory, and saves snapshots to a log file.

You will not be writing everything from scratch. Most of the code is provided for you. Your job is to fill in the important missing pieces, marked with `TODO` comments and blanks like `________`. Read the hints, think about what the blank needs, and type your answer in place of the blank.

> **How to use this tutorial**
>
> - Go in order. Each Part builds on the one before it.
> - Type the code yourself instead of copying and pasting. You will learn much more.
> - Run every test before moving on. Small mistakes are much easier to fix early.
> - When you see a **Git Checkpoint**, actually do it. This builds your GitHub history.
> - Replace every `____` blank. A blank left in your code will cause an error (see Part 14).

---

## Table of Contents

- [Part 1: Understand the Project](#part-1-understand-the-project)
- [Part 2: Create the GitHub Repository and Clone It](#part-2-create-the-github-repository-and-clone-it)
- [Part 3: Set Up Python, psutil, and the Project Files](#part-3-set-up-python-psutil-and-the-project-files)
- [Part 4: Build Basic System Information](#part-4-build-basic-system-information)
- [Part 5: Monitor CPU, Memory, and Disk](#part-5-monitor-cpu-memory-and-disk)
- [Part 6: Build the Resource Summary](#part-6-build-the-resource-summary)
- [Part 7: Add Resource Warnings](#part-7-add-resource-warnings)
- [Part 8: Build the Live Monitor](#part-8-build-the-live-monitor)
- [Part 9: Find the Top Processes](#part-9-find-the-top-processes)
- [Part 10: Save Resource Snapshots](#part-10-save-resource-snapshots)
- [Part 11: Build the Main Menu](#part-11-build-the-main-menu)
- [Part 12: Test the Complete Project](#part-12-test-the-complete-project)
- [Part 13: Write Your README and Submit](#part-13-write-your-readme-and-submit)
- [Part 14: Troubleshooting](#part-14-troubleshooting)
- [Part 15: Optional Extensions](#part-15-optional-extensions)
- [Final Knowledge Check](#final-knowledge-check)

---

## Part 1: Understand the Project

### Step 1.1: What you are building

When you finish, running your program will show a menu like this:

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

Each option does something real with your computer's information:

| Option | What it does |
|---|---|
| 1. View Current System Status | Shows CPU, memory, and disk usage, plus warnings if anything is high |
| 2. Start Live Monitor | Refreshes the numbers every 2 seconds until you press `Ctrl+C` |
| 3. View Top Processes | Lists the 5 programs using the most memory |
| 4. Save Current Snapshot | Saves the current numbers to a CSV log file |
| 5. View System Information | Shows your operating system, computer name, and processor |
| 6. Exit | Closes the program |

### Step 1.2: Key computer terms

You will see these words throughout the project.

- **CPU (Central Processing Unit):** The "brain" of the computer that runs instructions. **CPU usage** is the percentage of time the CPU is busy. 5% means it is mostly idle; 95% means it is working very hard.
- **Memory / RAM (Random Access Memory):** Fast, temporary storage that holds the programs and data you are using *right now*. It is cleared when the computer turns off. **Memory usage** is how much of your RAM is currently in use.
- **Disk / Storage:** Long-term storage (your SSD or hard drive) where files, apps, and the operating system are saved. It keeps data when the computer is off. **Disk usage** is how full your drive is.
- **Process:** A running program. When you open Chrome, VS Code, or Spotify, your computer creates one or more processes for it. Each process has a **PID (Process ID)**, a unique number the operating system uses to identify it.
- **Byte / GB:** Computers measure memory and storage in **bytes**. A **gigabyte (GB)** is about one billion bytes. You will convert bytes to GB so the numbers are readable.

### Step 1.3: Key Python and tool terms

- **Python module:** A `.py` file containing code (functions, variables) that other files can use with `import`. Each file you create in this project is a module.
- **Library / package:** A collection of modules someone else wrote that you can install and use. You will use **`psutil`**, a library that reads system information (CPU, memory, disk, processes) on Windows, macOS, and Linux.
- **Standard library:** Modules that come built into Python, so you do not need to install them. You will use `platform`, `socket`, `os`, `time`, `csv`, and `datetime`.
- **Git:** A tool that tracks changes to your files over time, like a save history for your code.
- **GitHub:** A website that stores Git projects online so you can back them up, share them, and show them to employers.

### Step 1.4: How the project is organized

Your finished project folder will look like this:

```text
tb-system-resource-monitor/
│
├── main.py            <- The menu. You run this file.
├── monitor.py         <- Reads CPU, memory, disk, processes; warnings; live monitor
├── logger.py          <- Saves snapshots to a CSV file
│
├── logs/
│   └── .gitkeep       <- Empty file so Git keeps the logs folder
│
├── .gitignore         <- Tells Git which files NOT to track
├── README.md          <- Describes your project (you will write this in Part 13)
└── requirements.txt   <- Lists the libraries your project needs
```

Splitting the code into three files keeps each file focused on one job. `main.py` talks to the user, `monitor.py` collects information, and `logger.py` saves it.

---

## Part 2: Create the GitHub Repository and Clone It

Your project lives on GitHub from the very beginning. You will create it online first, then download (clone) it to your computer.

### Step 2.1: Git vocabulary

| Term | Meaning |
|---|---|
| **Repository (repo)** | A project folder that Git tracks. It holds your files and their full change history. |
| **Clone** | Download a copy of a GitHub repository to your computer, already connected to GitHub. |
| **Commit** | Save a snapshot of your changes *on your computer*, with a short message describing what changed. |
| **Push** | Upload your commits from your computer *to GitHub*. |
| **Pull** | Download new commits *from GitHub* to your computer (for example, if you edited a file on the GitHub website or on another computer). |

The most important idea: **a commit saves locally; a push sends it to GitHub.** If you commit but never push, your work is not on GitHub.

### Step 2.2: Before you start

Make sure you have:

1. A **GitHub account** (https://github.com).
2. **Git** installed. Open a terminal and run:

   ```bash
   git --version
   ```

   If you see a version number (like `git version 2.45.1`), you are good. If not, install Git from https://git-scm.com/downloads.

3. **VS Code** installed (https://code.visualstudio.com).

If this is your first time using Git on this computer, tell Git who you are (use the email connected to your GitHub account):

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Step 2.3: Create the repository on GitHub

1. Go to https://github.com and sign in.
2. Click the **+** button in the top-right corner, then **New repository**.
3. Fill in the form:
   - **Repository name:** `tb-system-resource-monitor`
   - **Description:** `A Python command-line system resource monitor built with psutil.`
   - **Visibility:** **Public** (this will go in your portfolio)
   - **Check** "Add a README file"
   - **.gitignore:** leave as **None** (you will write your own)
   - **License:** None is fine for now
4. Click **Create repository**.

You now have a repository online with one file: `README.md`.

### Step 2.4: Clone the repository into VS Code

1. On your repository's GitHub page, click the green **Code** button.
2. Make sure **HTTPS** is selected, then click the copy icon to copy the URL. It looks like:

   ```text
   https://github.com/YOUR-USERNAME/tb-system-resource-monitor.git
   ```

3. Open **VS Code**.
4. Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS) to open the Command Palette.
5. Type **Git: Clone** and press Enter.
6. Paste the URL and press Enter.
7. Choose a parent folder to save it in (for example, `Documents` or a `Projects` folder). VS Code will create a `tb-system-resource-monitor` folder inside it.
8. When VS Code asks **"Would you like to open the cloned repository?"**, click **Open**.

> **Alternative (terminal):** Navigate to the folder where you keep projects, then run:
>
> ```bash
> git clone https://github.com/YOUR-USERNAME/tb-system-resource-monitor.git
> ```
>
> Then in VS Code, use **File > Open Folder** and select the new `tb-system-resource-monitor` folder.

If VS Code or Git asks you to sign in to GitHub, follow the prompts and allow access.

### Step 2.5: Open the terminal and confirm

In VS Code, open the built-in terminal with **Terminal > New Terminal** (or `` Ctrl+` ``). The terminal should already be inside your project folder. Run:

```bash
git status
```

You should see something like:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

That means your folder is a Git repository connected to GitHub. From now on, **every project file goes inside this folder.**

---

## Part 3: Set Up Python, psutil, and the Project Files

### Step 3.1: Find your Python command

Different computers use different commands to run Python. In the VS Code terminal, try these until one prints a version of **3.8 or higher**:

**Windows:**

```bash
python --version
```

or

```bash
py --version
```

**macOS / Linux:**

```bash
python3 --version
```

> **Important:** Throughout this tutorial, `python` means *whichever command worked for you*. If `py` worked, type `py` everywhere you see `python`. If `python3` worked, type `python3`.

If none of these work, install Python from https://www.python.org/downloads/. On Windows, **check "Add python.exe to PATH"** during installation, then close and reopen VS Code.

**Also in VS Code:**

1. Install the **Python** extension (by Microsoft) from the Extensions panel.
2. Press `Ctrl+Shift+P` / `Cmd+Shift+P`, type **Python: Select Interpreter**, and choose the Python version you just confirmed.

### Step 3.2: What is a library, and why psutil?

Python by itself cannot easily ask your operating system "How busy is the CPU?" The answer is different on Windows, macOS, and Linux. The **`psutil`** library (short for "process and system utilities") handles those differences for you. You call one function, and psutil does the operating-system-specific work.

`psutil` is not part of the standard library, so you need to install it with **pip**, Python's package installer.

### Step 3.3: Install psutil

In the VS Code terminal, run the command that matches your Python command:

**Windows:**

```bash
python -m pip install psutil
```

or

```bash
py -m pip install psutil
```

**macOS / Linux:**

```bash
python3 -m pip install psutil
```

> **Why `python -m pip` instead of just `pip`?** It guarantees psutil is installed for the *same* Python you will use to run your program. Many "module not found" errors come from installing into a different Python.

Confirm it installed:

```bash
python -m pip show psutil
```

You should see `Name: psutil` and a version number. If you get an error about an "externally managed environment" on macOS or Linux, see Part 14.

### Step 3.4: Create the project files

In the VS Code **Explorer** panel (left side), make sure you are in the `tb-system-resource-monitor` folder. Create the following using the **New File** and **New Folder** buttons:

1. `main.py` (leave empty for now)
2. `monitor.py` (leave empty for now)
3. `logger.py` (leave empty for now)
4. `requirements.txt`
5. `.gitignore` (the name starts with a dot)
6. A folder named `logs`
7. Inside `logs`, a file named `.gitkeep` (leave it empty)

**Why `.gitkeep`?** Git only tracks *files*, not empty folders. An empty folder would never appear on GitHub. Putting an empty `.gitkeep` file inside makes Git keep the `logs` folder.

### Step 3.5: Fill in `requirements.txt`

**File:** `requirements.txt`

A `requirements.txt` file lists the libraries your project needs. Anyone who downloads your project can install them all with one command.

```text
# TODO:
# Replace this whole file with ONE line: the name of the library you installed in Step 3.3.
______
```

**Fill-in Hints**

- The file should contain only the library name, nothing else (delete the `# TODO` lines too).
- Do not add a version number.

Someone who clones your project later would install everything with:

```bash
python -m pip install -r requirements.txt
```

Try running that now. It should say psutil is already installed ("Requirement already satisfied").

### Step 3.6: Fill in `.gitignore`

**File:** `.gitignore`

A `.gitignore` file tells Git which files to **ignore** (never track or upload). This keeps junk and personal files out of your repository.

```text
# Python cache files (created automatically when Python runs)
__pycache__/
*.pyc

# Virtual environment (only if you created one)
.venv/
venv/

# Operating system / editor files
.DS_Store
Thumbs.db
.vscode/

# Personal test file
# TODO: Add the name of the test file you will use in Part 4 (scratch.py)
__________

# Generated snapshot logs (keep the folder, ignore the data)
# TODO: Ignore every file ending in .csv inside the logs folder
__________
```

**Fill-in Hints**

- You will use a file called `scratch.py` for quick tests. It is personal, so Git should ignore it.
- `*` means "anything." For example, `*.pyc` means "every file ending in `.pyc`."
- To ignore all CSV files in the `logs` folder, combine the folder name, a `/`, and a `*` pattern.

**Why ignore the CSV logs?** The snapshot files are *generated* by running your program and contain data about *your* computer. They change every time you run the program, they are different on every machine, and they are not source code. We keep the folder (thanks to `.gitkeep`) but ignore the data inside it.

### Git Checkpoint 1

Now save this setup to GitHub.

```bash
git status
```

You should see your new files listed in red as "untracked." (`main.py`, `monitor.py`, and `logger.py` will appear even though they are empty.)

```bash
git add .
git commit -m "Set up project files, requirements, and gitignore"
git push
```

- `git add .` stages all your changes (the `.` means "everything in this folder").
- `git commit -m "..."` saves a snapshot with a message.
- `git push` uploads it to GitHub.

Refresh your repository page on GitHub. You should see your files, including the `logs` folder.

---

## Part 4: Build Basic System Information

Now you will start writing Python. You will build two functions that collect and display basic facts about your computer.

### Step 4.1: Start `monitor.py` with imports

**File:** `monitor.py`

An **import** loads a module so you can use its functions. Imports always go at the **top** of the file.

Type this at the top of `monitor.py`:

```python
"""
monitor.py

System information, resource monitoring, warnings, live monitor,
and process information for the TB System Resource Monitor.
"""

import os
import platform
import socket
import time

import psutil


# -------------------------------------------------------------------
# Settings (constants)
# -------------------------------------------------------------------

# You will add settings here in Parts 5, 7, and 8.


# -------------------------------------------------------------------
# Part 4: System information
# -------------------------------------------------------------------
```

What each import is for:

| Module | Type | Used for |
|---|---|---|
| `os` | Standard library | Checking files/paths and clearing the screen |
| `platform` | Standard library | Operating system and processor info |
| `socket` | Standard library | The computer's name (hostname) |
| `time` | Standard library | Pausing the live monitor |
| `psutil` | Installed library | CPU, memory, disk, and process info |

The text in triple quotes (`"""..."""`) at the top is a **docstring**, a description of the file. Lines starting with `#` are **comments**. Python ignores both; they are notes for humans.

### Step 4.2: What is a dictionary?

A **dictionary** stores data as **key-value pairs**. Instead of remembering "the hostname is the 3rd item," you look it up by name.

```python
student = {
    "name": "Jordan",
    "year": 2,
    "major": "Computer Science",
}

print(student["name"])   # prints: Jordan
student["year"] = 3      # changes the value for "year"
```

- Keys (like `"name"`) go on the left of the `:`.
- Values (like `"Jordan"`) go on the right.
- You read a value with `dictionary_name["key"]`.

You will use dictionaries throughout this project to group related information together.

### Step 4.3: Write `get_system_info()`

**File:** `monitor.py` (add below the "Part 4" comment)

A **function** is a named, reusable block of code. You define it with `def`. A function can **return** a value, which hands the result back to whoever called it.

```python
def get_system_info():
    """
    Return a dictionary of basic information about this computer.
    """

    info = {
        # TODO: Use platform.system() to get the operating system name.
        "os_name": ______________________,

        "os_release": platform.release(),

        # TODO: Use socket.gethostname() to get the computer's name.
        "hostname": ______________________,

        # TODO: Use platform.processor() to get the processor description.
        "processor": ______________________,

        "python_version": platform.python_version(),
    }

    # Some computers report an empty processor string.
    # TODO: Check whether the processor value is an empty string ("").
    if info["processor"] == ______:
        info["processor"] = "Not available"

    # TODO: Return the dictionary.
    return ______
```

**Fill-in Hints**

- Useful functions: `platform.system()`, `socket.gethostname()`, `platform.processor()`
- Do not forget the parentheses `()` when calling a function. `platform.system` without `()` is the function itself, not its result.
- An empty string is written as two quotation marks with nothing between them.
- The variable holding the dictionary is named `info`.

**Why might processor be empty?** Processor information is reported differently by each operating system. On some Linux and macOS machines, `platform.processor()` returns nothing. Your code handles that instead of showing a blank.

### Step 4.4: Write `display_system_info()`

**File:** `monitor.py` (add below `get_system_info()`)

This function *uses* the dictionary from `get_system_info()` and prints it nicely.

```python
def display_system_info():
    """
    Print the system information in a readable format.
    """

    # TODO: Call get_system_info() and store the dictionary it returns.
    info = ______________________

    print()
    print("System Information")
    print("-" * 30)

    # TODO: Fill in the dictionary keys from get_system_info().
    print(f"Operating System: {info['os_name']} {info['__________']}")
    print(f"Computer Name:    {info['__________']}")
    print(f"Processor:        {info['__________']}")
    print(f"Python Version:   {info['python_version']}")
```

**Fill-in Hints**

- Call your own function the same way you call any other: name plus `()`.
- The keys must exactly match the keys you used in `get_system_info()`: `"os_name"`, `"os_release"`, `"hostname"`, `"processor"`, `"python_version"`.
- Inside an f-string that uses double quotes, use **single quotes** for dictionary keys, like `info['os_name']`.

**What is an f-string?** A string that starts with `f` lets you put variables inside `{}`:

```python
name = "Jordan"
print(f"Hello, {name}!")   # Hello, Jordan!
```

`"-" * 30` repeats the `-` character 30 times to make a divider line.

### Step 4.5: Test your system information

You will test your code with a personal file named `scratch.py`. (Your `.gitignore` already ignores it.)

1. Create a new file `scratch.py` in your project folder (same folder as `monitor.py`).
2. Type:

```python
import monitor

info = monitor.get_system_info()
print(info)

monitor.display_system_info()
```

3. Save **both** files, then run in the terminal:

```bash
python scratch.py
```

**Expected output** (yours will show your own computer):

```text
{'os_name': 'Windows', 'os_release': '11', 'hostname': 'JORDAN-LAPTOP', 'processor': 'Intel64 Family 6 Model 154 Stepping 3, GenuineIntel', 'python_version': '3.12.4'}

System Information
------------------------------
Operating System: Windows 11
Computer Name:    JORDAN-LAPTOP
Processor:        Intel64 Family 6 Model 154 Stepping 3, GenuineIntel
Python Version:   3.12.4
```

On macOS, `os_name` will be `Darwin` (the name of macOS's core system). On Linux, it will be `Linux`.

**Check:**

- [ ] The first line is a dictionary with 5 keys.
- [ ] Every line of the display has a value (Processor may say `Not available`, which is fine).
- [ ] No error messages.

> `import monitor` works because `scratch.py` and `monitor.py` are in the same folder. Python finds `monitor.py` and loads it as a module.

### Git Checkpoint 2

```bash
git status
git add .
git commit -m "Add system information functions"
git push
```

Notice that `scratch.py` does **not** appear in `git status`. That is your `.gitignore` working.

---

## Part 5: Monitor CPU, Memory, and Disk

### Step 5.1: Bytes to gigabytes

psutil reports memory and disk sizes in **bytes**, which produces huge numbers like `17179869184`. You will convert them to gigabytes.

In computing, sizes are counted in powers of 1024:

```text
1 KB = 1024 bytes
1 MB = 1024 KB = 1024 * 1024 bytes
1 GB = 1024 MB = 1024 * 1024 * 1024 bytes  =  1024 ** 3 bytes
```

In Python, `**` means "to the power of." So `1024 ** 3` means 1024 x 1024 x 1024.

> You might notice your computer's "16 GB" of RAM shows as something like 15.8 GB. That is normal. Some memory is reserved by hardware, and manufacturers sometimes use 1000 instead of 1024.

**File:** `monitor.py`, in the **Settings** section near the top. Replace the line `# You will add settings here in Parts 5, 7, and 8.` with:

```python
# 1 GB = 1024 * 1024 * 1024 bytes
# TODO: Fill in the exponent so this equals the number of bytes in 1 GB.
BYTES_PER_GB = 1024 ** ___
```

Names in ALL CAPS are **constants**: values that are set once and are not supposed to change while the program runs.

### Step 5.2: Write `bytes_to_gb()`

**File:** `monitor.py`. First add a new section comment at the bottom of the file, then the function:

```python
# -------------------------------------------------------------------
# Part 5: CPU, memory, and disk
# -------------------------------------------------------------------

def bytes_to_gb(num_bytes):
    """
    Convert a number of bytes to gigabytes, rounded to 2 decimal places.
    """

    # TODO: Divide the number of bytes by the number of bytes in 1 GB.
    gigabytes = __________ / __________

    # TODO: Round gigabytes to 2 decimal places.
    return round(__________, ___)
```

**Fill-in Hints**

- `num_bytes` is a **parameter**: a value passed into the function when it is called. For example, `bytes_to_gb(2147483648)` sets `num_bytes` to `2147483648`.
- Use the constant you created in Step 5.1.
- `round(value, digits)` rounds a number. For example, `round(3.14159, 2)` gives `3.14`.

### Step 5.3: Write `get_cpu_usage()`

**File:** `monitor.py` (add below `bytes_to_gb()`)

```python
def get_cpu_usage():
    """
    Return the current CPU usage percentage.
    """

    # TODO:
    # Use psutil.cpu_percent().
    # Use an interval of 1 second.
    cpu_usage = ______________________________

    # TODO: Return the CPU usage.
    return __________________
```

**Fill-in Hints**

- Useful function: `psutil.cpu_percent()`
- The `interval` argument tells psutil how long to measure CPU usage, in seconds. Pass it by name, like `some_function(interval=5)`.
- **Why an interval?** CPU usage is "how busy was the CPU *over a period of time*." psutil watches the CPU for 1 second, then reports the percentage. This means the function takes about 1 second to run. That is expected.

### Step 5.4: Test CPU usage

Replace everything in `scratch.py` with:

```python
import monitor

print("Bytes test:", monitor.bytes_to_gb(2147483648))
print("CPU usage:", monitor.get_cpu_usage())
```

Run:

```bash
python scratch.py
```

**Expected output** (CPU number will vary):

```text
Bytes test: 2.0
CPU usage: 7.3
```

**Check:**

- [ ] The bytes test prints exactly `2.0` (2147483648 bytes is exactly 2 GB).
- [ ] CPU usage is a decimal number (a **float**) between `0.0` and `100.0`.
- [ ] There is about a 1-second pause before the CPU line appears.

Try opening a few heavy programs or a video and running it again. The number should change. (A value of `0.0` on an idle computer can happen and is fine.)

### Step 5.5: Write `get_memory_usage()`

`psutil.virtual_memory()` returns an object full of memory information. You read pieces of it with a dot, like `memory.total`. The pieces you need:

| Attribute | Meaning | Unit |
|---|---|---|
| `.total` | Total RAM installed | bytes |
| `.used` | RAM currently in use | bytes |
| `.percent` | Percentage of RAM in use | percent (0-100) |

**File:** `monitor.py` (add below `get_cpu_usage()`)

```python
def get_memory_usage():
    """
    Return a dictionary with memory (RAM) percent, used GB, and total GB.
    """

    # TODO: Call psutil.virtual_memory() and store the result.
    memory = ______________________________

    memory_info = {
        # TODO: Use the .percent attribute of memory.
        "percent": memory.__________,

        # TODO: Convert memory.used from bytes to GB using your function.
        "used_gb": ______________(memory.used),

        # TODO: Convert the total memory from bytes to GB.
        "total_gb": bytes_to_gb(______________),
    }

    return memory_info
```

**Fill-in Hints**

- Useful function: `psutil.virtual_memory()`
- `memory.percent` is already a percentage, so it does not need converting.
- `.used` and `.total` are in bytes, so pass them to `bytes_to_gb()`.

### Step 5.6: Write `get_disk_path()`

To measure disk usage, psutil needs to know *which* disk. The main drive has a different path on each operating system:

| Operating system | `platform.system()` returns | Main disk path |
|---|---|---|
| Windows | `"Windows"` | `C:\` |
| macOS | `"Darwin"` | `/System/Volumes/Data` (where your files live on modern macOS) |
| Linux | `"Linux"` | `/` |

**File:** `monitor.py` (add below `get_memory_usage()`)

```python
def get_disk_path():
    """
    Return the path of the main disk for this operating system.
    """

    # TODO: Get the name of the operating system (same function as Part 4).
    system_name = ______________________

    # TODO: Fill in the name platform.system() returns on Windows.
    if system_name == "__________":
        return "C:\\"
    elif system_name == "Darwin" and os.path.exists("/System/Volumes/Data"):
        # On modern macOS, your files live on the "Data" volume.
        return "/System/Volumes/Data"
    else:
        # TODO: Return the root path used by Linux (and older macOS).
        return "___"
```

**Fill-in Hints**

- You already used `platform.system()` in Step 4.3.
- Capitalization matters: `"windows"` and `"Windows"` are different strings.
- The Linux root path is a single forward slash.
- **Why `"C:\\"` with two backslashes?** In Python strings, `\` is a special "escape" character. Writing `\\` produces one real backslash, so `"C:\\"` means `C:\`.
- `if` / `elif` / `else` is a **conditional**: Python checks each condition in order and runs the first block whose condition is true. `elif` means "else if."

### Step 5.7: Write `get_disk_usage()`

`psutil.disk_usage(path)` works just like `virtual_memory()`: it returns an object with `.total`, `.used`, and `.percent`.

**File:** `monitor.py` (add below `get_disk_path()`)

```python
def get_disk_usage():
    """
    Return a dictionary with disk percent, used GB, and total GB.
    """

    # TODO: Call psutil.disk_usage() and pass it the path from get_disk_path().
    disk = psutil.disk_usage(____________________)

    # TODO: Build the dictionary the same way you did in get_memory_usage().
    disk_info = {
        "percent": ____________________,
        "used_gb": ____________________,
        "total_gb": ____________________,
    }

    return disk_info
```

**Fill-in Hints**

- You can call a function *inside* another function call: `psutil.disk_usage(get_disk_path())`.
- Look back at `get_memory_usage()`. This dictionary follows the exact same pattern, but uses `disk` instead of `memory`.
- Remember to convert `.used` and `.total` with `bytes_to_gb()`.

### Step 5.8: Test memory and disk

Replace everything in `scratch.py` with:

```python
import monitor

memory = monitor.get_memory_usage()
print("Memory:", memory)

print("Disk path:", monitor.get_disk_path())
disk = monitor.get_disk_usage()
print("Disk:", disk)
```

Run `python scratch.py`.

**Expected output** (numbers will vary):

```text
Memory: {'percent': 61.8, 'used_gb': 9.89, 'total_gb': 15.73}
Disk path: C:\
Disk: {'percent': 72.1, 'used_gb': 331.42, 'total_gb': 460.72}
```

**Check:**

- [ ] Both `percent` values are between `0` and `100`.
- [ ] `total_gb` for memory is close to your computer's RAM (often 8, 16, or 32 GB).
- [ ] `total_gb` for disk is close to your drive size (often 256, 512, or 1000 GB).
- [ ] `used_gb` is less than `total_gb`.
- [ ] The disk path matches your operating system.

> **macOS note:** memory `used_gb` may look lower than `percent` suggests. macOS counts memory in a special way (compressed memory, cached files). The percentage is the most reliable number. This is normal.

### Git Checkpoint 3

```bash
git status
git add .
git commit -m "Add CPU, memory, and disk monitoring"
git push
```

---

## Part 6: Build the Resource Summary

Right now, getting all the numbers takes three separate function calls. You will build one function that collects everything into **one dictionary**. Other parts of your program (warnings, live monitor, logger) will all use this dictionary.

### Step 6.1: Write `get_resource_summary()`

**File:** `monitor.py`. Add a new section at the bottom:

```python
# -------------------------------------------------------------------
# Part 6: Resource summary
# -------------------------------------------------------------------

def get_resource_summary():
    """
    Gather CPU, memory, and disk information into ONE dictionary.
    """

    # TODO: Call your memory function and store its dictionary.
    memory = ______________________

    # TODO: Call your disk function and store its dictionary.
    disk = ______________________

    summary = {
        # TODO: Call your CPU function.
        "cpu_percent": ______________________,

        "memory_percent": memory["percent"],

        # TODO: Get the used GB value out of the memory dictionary.
        "memory_used_gb": memory["__________"],

        # TODO: Get the total GB value out of the memory dictionary.
        "memory_total_gb": ______________________,

        # TODO: Get the percent value out of the disk dictionary.
        "disk_percent": ______________________,

        "disk_used_gb": disk["used_gb"],

        # TODO: Get the total GB value out of the disk dictionary.
        "disk_total_gb": ______________________,
    }

    return summary
```

**Fill-in Hints**

- The three functions you need: `get_cpu_usage()`, `get_memory_usage()`, `get_disk_usage()`.
- `memory` and `disk` are dictionaries with the keys `"percent"`, `"used_gb"`, and `"total_gb"`.
- Read a value with `dictionary_name["key"]`. The completed lines `memory["percent"]` and `disk["used_gb"]` show the pattern.

**Why one dictionary?** It bundles every number with a clear name. Any function that needs resource data can take this one dictionary instead of seven separate values. It also measures everything at almost the same moment.

### Step 6.2: Write `display_resource_summary()`

**File:** `monitor.py` (add below `get_resource_summary()`)

This function takes a summary dictionary as a **parameter** and prints it.

```python
def display_resource_summary(summary):
    """
    Print a resource summary dictionary in a readable format.
    """

    print()
    print("Current System Status")
    print("-" * 30)
    print(f"CPU Usage:    {summary['cpu_percent']}%")

    # TODO: Fill in the correct summary keys.
    print(f"Memory Usage: {summary['______________']}%")
    print(f"Used Memory:  {summary['memory_used_gb']:.2f} GB")
    print(f"Total Memory: {summary['______________']:.2f} GB")
    print(f"Disk Usage:   {summary['______________']}%")
    print(f"Used Disk:    {summary['______________']:.2f} GB")
    print(f"Total Disk:   {summary['disk_total_gb']:.2f} GB")
```

**Fill-in Hints**

- Use the exact keys from the `summary` dictionary you built in Step 6.1.
- `:.2f` inside the `{}` means "show this number with exactly 2 decimal places." So `16.0` displays as `16.00`. It does not change the actual value, only how it is printed.

### Step 6.3: Test the summary

Replace everything in `scratch.py` with:

```python
import monitor

summary = monitor.get_resource_summary()
print(summary)

monitor.display_resource_summary(summary)
```

Run `python scratch.py`.

**Expected output:**

```text
{'cpu_percent': 12.4, 'memory_percent': 61.8, 'memory_used_gb': 9.89, 'memory_total_gb': 15.73, 'disk_percent': 72.1, 'disk_used_gb': 331.42, 'disk_total_gb': 460.72}

Current System Status
------------------------------
CPU Usage:    12.4%
Memory Usage: 61.8%
Used Memory:  9.89 GB
Total Memory: 15.73 GB
Disk Usage:   72.1%
Used Disk:    331.42 GB
Total Disk:   460.72 GB
```

**Check:**

- [ ] The dictionary has exactly 7 keys.
- [ ] Every line of the display shows a number.
- [ ] GB values show 2 decimal places.

### Git Checkpoint 4

```bash
git add .
git commit -m "Add resource summary dictionary and display"
git push
```

---

## Part 7: Add Resource Warnings

A monitor is more useful when it tells you something is wrong. You will compare each resource to a **threshold** (a limit) and show a warning if it goes above.

### Step 7.1: Add the thresholds

**File:** `monitor.py`, in the **Settings** section, below `BYTES_PER_GB`:

```python
# Warning thresholds (in percent)
# TODO: Fill in the default thresholds: CPU 80, memory 80, disk 90.
THRESHOLDS = {
    "cpu": ____,
    "memory": ____,
    "disk": ____,
}
```

**Fill-in Hints**

- Thresholds are plain numbers, with no `%` sign and no quotes.
- Storing them in one dictionary means you can change a limit in one place.

### Step 7.2: Write `check_status()`

**File:** `monitor.py`. Add a new section at the bottom:

```python
# -------------------------------------------------------------------
# Part 7: Warnings
# -------------------------------------------------------------------

def check_status(value, threshold):
    """
    Return "HIGH" if value is above threshold, otherwise "OK".
    """

    # TODO: Check whether value is greater than threshold.
    if __________ > __________:
        # TODO: Return the text "HIGH".
        return "__________"

    return "OK"
```

**Fill-in Hints**

- The two parameters are named `value` and `threshold`.
- `>` means "greater than."
- When a `return` runs, the function stops immediately. So if the value is high, the function returns `"HIGH"` and never reaches `return "OK"`.

### Step 7.3: Write `get_statuses()`

**File:** `monitor.py` (add below `check_status()`)

```python
def get_statuses(summary):
    """
    Return a dictionary with the status ("OK" or "HIGH") of each resource.
    """

    statuses = {
        "cpu": check_status(summary["cpu_percent"], THRESHOLDS["cpu"]),

        # TODO: Check memory_percent against the memory threshold.
        "memory": check_status(summary["______________"], THRESHOLDS["________"]),

        # TODO: Check disk_percent against the disk threshold.
        "disk": ______________(______________________, ______________________),
    }

    return statuses
```

**Fill-in Hints**

- Follow the completed `"cpu"` line exactly, changing only the keys.
- Summary keys: `"memory_percent"`, `"disk_percent"`. Threshold keys: `"memory"`, `"disk"`.

### Step 7.4: Write `get_warnings()`

A **list** stores items in order inside square brackets: `[]` is an empty list. `.append(item)` adds an item to the end.

```python
colors = []
colors.append("red")
colors.append("blue")
print(colors)   # ['red', 'blue']
```

**File:** `monitor.py` (add below `get_statuses()`)

```python
def get_warnings(summary):
    """
    Return a list of warning messages for any resource that is HIGH.
    """

    warnings = []
    statuses = get_statuses(summary)

    if statuses["cpu"] == "HIGH":
        warnings.append("WARNING: CPU usage is high!")

    # TODO: Check the memory status and add the memory warning.
    if statuses["__________"] == "HIGH":
        warnings.__________("WARNING: Memory usage is high!")

    # TODO: Check the disk status and add the disk warning.
    #       Write the full if statement, following the two above.
    if ______________________ == "______":
        warnings.append("______________________________")

    return warnings
```

**Fill-in Hints**

- `==` checks whether two values are equal (one `=` assigns a value; two `==` compares).
- Follow the CPU `if` block as your pattern.
- The disk message should be exactly: `WARNING: Disk usage is high!`
- These are three separate `if` statements (not `elif`) because more than one resource can be high at the same time.

### Step 7.5: Write `display_warnings()`

**File:** `monitor.py` (add below `get_warnings()`)

```python
def display_warnings(summary):
    """
    Print each warning, or a friendly message if there are none.
    """

    warnings = get_warnings(summary)

    # TODO: Check whether the warnings list is empty (has length 0).
    if len(warnings) == ___:
        print("All resources are within normal limits.")
    else:
        # TODO: Loop through each warning in the list and print it.
        for __________ in __________:
            print(warning)
```

**Fill-in Hints**

- `len(some_list)` returns how many items are in a list.
- A `for` loop repeats code once for each item in a list: `for item in my_list:`. The variable after `for` holds the current item. Look at the `print` line to see what this variable must be named.

### Step 7.6: Test the warnings

**Test 1: Normal thresholds.** Replace everything in `scratch.py` with:

```python
import monitor

summary = monitor.get_resource_summary()
print("Statuses:", monitor.get_statuses(summary))
monitor.display_warnings(summary)
```

Run it. Unless your computer is very busy, you should see:

```text
Statuses: {'cpu': 'OK', 'memory': 'OK', 'disk': 'OK'}
All resources are within normal limits.
```

**Test 2: Force a warning.** In `monitor.py`, **temporarily** change the memory threshold to `1`:

```python
    "memory": 1,
```

Save and run `scratch.py` again. Now you should see:

```text
Statuses: {'cpu': 'OK', 'memory': 'HIGH', 'disk': 'OK'}
WARNING: Memory usage is high!
```

(Memory is always above 1%, so this reliably triggers. If you want, try setting all three thresholds to `1` and confirm you get multiple warnings.)

> **IMPORTANT:** Change the threshold(s) **back to the normal values** (CPU `80`, memory `80`, disk `90`) before moving on. Run the test once more to confirm everything says `OK` again.

**Check:**

- [ ] With normal thresholds, you see "All resources are within normal limits." (or a real warning if your disk really is over 90% full!)
- [ ] With a 1% threshold, the warning appears.
- [ ] Thresholds are restored to 80 / 80 / 90.

### Git Checkpoint 5

```bash
git add .
git commit -m "Add resource warnings with thresholds"
git push
```

---

## Part 8: Build the Live Monitor

The live monitor refreshes the numbers every few seconds, forever, until you press `Ctrl+C`.

### Step 8.1: Loops and refresh time

A **`while` loop** repeats its code *as long as* its condition is true. `while True:` creates a loop that repeats forever:

```python
count = 0
while True:
    print(count)
    count = count + 1
```

That would print numbers forever. For a live monitor, "forever" is exactly what you want: gather data, show it, wait, repeat. The user stops it with `Ctrl+C`.

`time.sleep(seconds)` pauses the program for that many seconds. Without it, the loop would refresh as fast as possible and flicker constantly.

**File:** `monitor.py`, in the **Settings** section, below `THRESHOLDS`:

```python
# How many seconds the live monitor waits between refreshes
# TODO: Set this to 2 seconds.
REFRESH_SECONDS = ___
```

### Step 8.2: Write `clear_screen()`

To make the display update in place, you clear the terminal before each refresh. The command is different on each operating system: `cls` on Windows, `clear` on macOS and Linux.

`os.name` is `"nt"` on Windows and `"posix"` on macOS/Linux. `os.system("command")` runs a terminal command.

**File:** `monitor.py`. Add a new section at the bottom:

```python
# -------------------------------------------------------------------
# Part 8: Live monitor
# -------------------------------------------------------------------

def clear_screen():
    """
    Clear the terminal window.
    """

    # os.name is "nt" on Windows
    # TODO: Fill in the value of os.name on Windows,
    #       and the Windows clear-screen command.
    if os.name == "______":
        os.system("______")
    else:
        os.system("clear")
```

**Fill-in Hints**

- Both answers are in the explanation above this code.
- Both are short lowercase strings.

### Step 8.3: Write `display_live_screen()`

**File:** `monitor.py` (add below `clear_screen()`)

This prints one "frame" of the live monitor.

```python
def display_live_screen(summary):
    """
    Print one "frame" of the live monitor.
    """

    # TODO: Get the statuses dictionary for this summary.
    statuses = ______________(summary)

    print("=" * 30)
    print("   TB System Resource Monitor")
    print("=" * 30)
    print()
    print(f"CPU Usage:      {summary['cpu_percent']}%")
    print(f"Memory Usage:   {summary['memory_percent']}%")

    # TODO: Print the disk percent from the summary.
    print(f"Disk Usage:     {summary['______________']}%")
    print()
    print("Status:")
    print(f"CPU:    {statuses['cpu']}")

    # TODO: Print the memory and disk statuses.
    print(f"Memory: {statuses['__________']}")
    print(f"Disk:   {statuses['__________']}")
    print()
    print("Press Ctrl+C to stop monitoring.")
```

**Fill-in Hints**

- You built a function in Part 7 that turns a summary into a statuses dictionary.
- The `statuses` dictionary has the keys `"cpu"`, `"memory"`, and `"disk"`.

### Step 8.4: Exceptions and `try/except`

When something goes wrong while Python is running, it **raises an exception** (an error). If nothing handles it, the program crashes and prints a long error message called a **traceback**.

A `try/except` block lets you **catch** an exception and handle it gracefully:

```python
try:
    number = int(input("Enter a number: "))
    print("You entered", number)
except ValueError:
    print("That was not a number!")
```

If the code inside `try` raises a `ValueError`, Python jumps to the `except ValueError:` block instead of crashing.

Pressing **`Ctrl+C`** in a terminal raises an exception called **`KeyboardInterrupt`**. Without handling, it prints an ugly traceback. You will catch it so the live monitor stops cleanly.

### Step 8.5: Write `start_live_monitor()`

**File:** `monitor.py` (add below `display_live_screen()`)

```python
def start_live_monitor():
    """
    Keep refreshing the screen until the user presses Ctrl+C.
    """

    try:
        # TODO: Start a loop that runs forever.
        while __________:
            # TODO: Gather a fresh resource summary.
            summary = ______________________

            clear_screen()

            # TODO: Display this summary on the screen.
            display_live_screen(__________)

            # TODO: Wait REFRESH_SECONDS seconds before the next refresh.
            time.__________(______________)

    # TODO: Catch the exception raised when the user presses Ctrl+C.
    except ______________________:
        print()
        print("Live monitor stopped. Returning to the menu...")
```

**Fill-in Hints**

- The condition for a loop that never ends on its own is `True` (capital T).
- Use `get_resource_summary()` from Part 6.
- Use the pause function from the `time` module described in Step 8.1, with your `REFRESH_SECONDS` constant.
- The exception name is in Step 8.4. Spelling and capitalization must be exact.
- **Why gather the summary *before* clearing the screen?** `get_resource_summary()` takes about 1 second (because of the CPU interval). If you cleared first, the screen would sit blank for that second. Gathering first makes the update look instant.

### Step 8.6: Test the live monitor

Replace everything in `scratch.py` with:

```python
import monitor

monitor.start_live_monitor()
print("Back in scratch.py - the program did not crash!")
```

Run `python scratch.py`. You should see:

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

Watch for 10 seconds or so, then press **`Ctrl+C`**.

```text
Live monitor stopped. Returning to the menu...
Back in scratch.py - the program did not crash!
```

**Check:**

- [ ] The screen clears and redraws about every 3 seconds (2 seconds of sleep + about 1 second to measure CPU).
- [ ] The CPU number changes between refreshes.
- [ ] `Ctrl+C` prints the "stopped" message, **not** a traceback.
- [ ] The final "Back in scratch.py" line prints, proving the program continued after the monitor stopped.

> On macOS, `Ctrl+C` is the **Control** key, not Command.

### Git Checkpoint 6

```bash
git add .
git commit -m "Add live monitor with Ctrl+C handling"
git push
```

---

## Part 9: Find the Top Processes

### Step 9.1: Why reading processes can fail

Your computer is running many processes at once (often 100-400). psutil can list them all with `psutil.process_iter()`, which gives you one **process object** at a time. Each process object has:

| What you want | How to get it | Notes |
|---|---|---|
| PID | `process.pid` | An attribute (no parentheses) |
| Name | `process.name()` | A method (needs parentheses) |
| Memory percent | `process.memory_percent()` | A method (needs parentheses) |

Reading process information can **fail**, and that is normal:

- **`psutil.NoSuchProcess`:** The process ended between the moment psutil listed it and the moment you asked for its details. Processes start and stop constantly.
- **`psutil.AccessDenied`:** The operating system will not let a normal user read that process. This often happens with system processes owned by the administrator or other users. You are **not** going to run as administrator, so you will just skip these.
- **`psutil.ZombieProcess`:** The process has finished but has not been fully cleaned up yet (mostly on macOS/Linux).

If you do not handle these, **one** inaccessible process would crash your **whole** program. Instead, you will catch these exceptions and skip that process.

### Step 9.2: Sorting a list of dictionaries

You will build a **list of dictionaries**, one dictionary per process:

```python
processes = [
    {"pid": 1234, "name": "chrome.exe", "memory_percent": 8.2},
    {"pid": 8910, "name": "Spotify.exe", "memory_percent": 2.1},
    {"pid": 4321, "name": "Code.exe", "memory_percent": 5.7},
]
```

To find the biggest memory users, you **sort** this list by memory percent, largest first. Python's `list.sort()` can take a `key`: a function that tells it *what to sort by*. You give `sort()` the function's **name** (no parentheses), and `sort()` calls it on each item for you.

```python
def get_age(person):
    return person["age"]

people.sort(key=get_age)                 # youngest first
people.sort(key=get_age, reverse=True)   # oldest first
```

**Slicing** gets part of a list: `my_list[:5]` gives the first 5 items.

### Step 9.3: Write `get_memory_value()`

**File:** `monitor.py`. Add a new section at the bottom:

```python
# -------------------------------------------------------------------
# Part 9: Top processes
# -------------------------------------------------------------------

def get_memory_value(process_info):
    """
    Return the memory percent from one process dictionary.
    Used as the "key" when sorting.
    """

    # TODO: Return the value stored under the "memory_percent" key.
    return process_info["______________"]
```

**Fill-in Hints**

- This works exactly like `get_age()` in Step 9.2.

### Step 9.4: Write `get_top_processes()`

**File:** `monitor.py` (add below `get_memory_value()`)

```python
def get_top_processes(limit=5):
    """
    Return a list of the processes using the most memory.
    Each item in the list is a dictionary.
    """

    # TODO: Start with an empty list.
    processes = ______

    # TODO: Loop over every running process using psutil.
    for process in ______________________:
        try:
            process_info = {
                # TODO: Fill in the attribute/methods from the table in Step 9.1.
                "pid": process.__________,
                "name": process.__________(),
                "memory_percent": process.______________(),
            }

            # TODO: Add process_info to the end of the processes list.
            processes.__________(process_info)

        # TODO: Catch the three psutil exceptions from Step 9.1.
        except (psutil.______________, psutil.______________, psutil.______________):
            # The process ended, or we are not allowed to read it.
            # TODO: Skip this process and move on to the next one.
            __________

    # TODO: Sort by memory percent, largest first.
    processes.sort(key=______________, reverse=______)

    # TODO: Return only the first `limit` items.
    return processes[:__________]
```

**Fill-in Hints**

- An empty list is `[]`.
- Useful function: `psutil.process_iter()`
- Check the table in Step 9.1 carefully: `pid` has **no** parentheses, while `name()` and `memory_percent()` do (the parentheses are already written for you).
- You used `.append()` in Step 7.4.
- Exception names: `NoSuchProcess`, `AccessDenied`, `ZombieProcess`. Putting several in parentheses catches any of them.
- The keyword `continue` skips the rest of the current loop repetition and goes to the next item.
- `key=` gets the **name** of your function from Step 9.3, with **no** parentheses.
- `reverse=True` sorts from largest to smallest.
- `limit=5` in the `def` line is a **default parameter**: if no value is passed, `limit` is 5.

### Step 9.5: Write `display_top_processes()`

**File:** `monitor.py` (add below `get_top_processes()`)

```python
def display_top_processes(limit=5):
    """
    Print the top processes in a table.
    """

    # TODO: Get the top processes, passing along limit.
    top_processes = ______________________(limit)

    print()
    print("Top Processes by Memory")
    print()
    print(f"{'PID':<8} {'Name':<25} {'Memory':>8}")
    print("-" * 43)

    for process_info in top_processes:
        # TODO: Read the pid and memory_percent from the dictionary.
        pid = process_info["__________"]
        name = process_info["name"][:25]
        memory = process_info["______________"]

        print(f"{pid:<8} {name:<25} {memory:>7.1f}%")
```

**Fill-in Hints**

- Call the function from Step 9.4.
- Use the keys you created in `process_info`: `"pid"`, `"name"`, `"memory_percent"`.

**About the formatting (already written for you):**

- `:<8` means "left-align in a space 8 characters wide," which lines up the columns.
- `:>7.1f` means "right-align in 7 characters, with 1 decimal place."
- `[:25]` cuts long process names to 25 characters so they do not break the table.

### Step 9.6: Test the top processes

Replace everything in `scratch.py` with:

```python
import monitor

all_processes = monitor.get_top_processes(1000)
print("Processes read successfully:", len(all_processes))

monitor.display_top_processes()
```

Run `python scratch.py`.

**Expected output** (yours will show your own programs):

```text
Processes read successfully: 214

Top Processes by Memory

PID      Name                        Memory
-------------------------------------------
1234     chrome.exe                    8.2%
4321     Code.exe                      5.7%
8910     Spotify.exe                   2.1%
2210     explorer.exe                  1.6%
5512     Discord.exe                   1.4%
```

**Check:**

- [ ] The count is more than a handful (usually dozens to hundreds).
- [ ] Exactly 5 processes are listed.
- [ ] They are in order from highest to lowest memory.
- [ ] No traceback, even though some system processes cannot be accessed.

> Some processes (like Chrome) appear several times with different PIDs. Modern browsers run many processes. That is expected.

### Git Checkpoint 7

```bash
git add .
git commit -m "Add top processes by memory with error handling"
git push
```

---

## Part 10: Save Resource Snapshots

### Step 10.1: What is CSV?

**CSV (Comma-Separated Values)** is a simple text format for tables. Each line is a row, and commas separate the columns. The first line is usually a **header** with column names:

```text
timestamp,cpu_percent,memory_percent,disk_percent
2026-10-27 18:30:00,32.5,61.7,72.3
2026-10-27 18:35:12,18.9,60.2,72.3
```

Excel, Google Sheets, and almost every data tool can open CSV files. Python's built-in **`csv`** module reads and writes them correctly for you.

A **timestamp** records *when* each row was saved. Without it, a log full of numbers would be useless, because you could not tell when anything happened.

### Step 10.2: Start `logger.py`

**File:** `logger.py`

```python
"""
logger.py

Saves resource snapshots to a CSV file for the TB System Resource Monitor.
"""

import csv
import os
from datetime import datetime


# The folder that contains this file (your project folder)
PROJECT_FOLDER = os.path.dirname(os.path.abspath(__file__))

# logs/ folder inside the project folder
LOG_FOLDER = os.path.join(PROJECT_FOLDER, "logs")

# logs/snapshots.csv
LOG_FILE = os.path.join(LOG_FOLDER, "snapshots.csv")

# The column names (header row) of the CSV file
FIELDNAMES = ["timestamp", "cpu_percent", "memory_percent", "disk_percent"]
```

What this does:

- `from datetime import datetime` imports just the `datetime` tool from the `datetime` module, so you can write `datetime.now()`.
- `__file__` is the path of the current file (`logger.py`). `PROJECT_FOLDER` is the folder it lives in. This makes sure the log always goes into **your project's** `logs` folder, no matter which folder your terminal is in.
- `os.path.join()` combines folder and file names using the correct separator for your operating system (`\` on Windows, `/` on macOS/Linux).

### Step 10.3: Write `get_timestamp()`

**File:** `logger.py` (add at the bottom)

```python
def get_timestamp():
    """
    Return the current date and time as text, like "2026-10-27 18:30:00".
    """

    # TODO: Get the current date and time using datetime.now().
    now = datetime.__________()

    return now.strftime("%Y-%m-%d %H:%M:%S")
```

**Fill-in Hints**

- Useful function: `datetime.now()`
- `strftime()` turns a date into text using a pattern. `%Y` = 4-digit year, `%m` = month, `%d` = day, `%H` = hour (24-hour), `%M` = minute, `%S` = second.

### Step 10.4: Write `needs_header()`

The CSV header should be written **only once**, when the file is new. If you wrote it every time, your file would have a header between every row.

**File:** `logger.py` (add below `get_timestamp()`)

```python
def needs_header():
    """
    Return True if the CSV file still needs a header row.
    """

    # The file does not exist yet
    # TODO: Use os.path.exists() to check whether LOG_FILE exists.
    if not os.path.__________(LOG_FILE):
        # TODO: The file is missing, so it needs a header.
        return __________

    # The file exists but is empty
    # TODO: Check whether the file size is 0 bytes.
    if os.path.getsize(LOG_FILE) == ___:
        return True

    return False
```

**Fill-in Hints**

- Useful function: `os.path.exists(path)` returns `True` if the file exists.
- `not` flips `True` to `False` and `False` to `True`. So `if not os.path.exists(...)` means "if the file does **not** exist."
- `True` and `False` are capitalized in Python.
- `os.path.getsize(path)` returns a file's size in bytes. An empty file has a size of 0.

### Step 10.5: Write `save_snapshot()`

**Opening files:** `open(path, mode)` opens a file. The **mode** decides what you can do:

| Mode | Meaning |
|---|---|
| `"r"` | Read only |
| `"w"` | Write (**erases** the file first!) |
| `"a"` | Append (adds to the **end** of the file, creates it if needed) |

You want `"a"` so each snapshot is **added** without erasing the old ones.

A `with open(...) as csv_file:` block automatically closes the file when the block ends, even if an error happens.

`csv.DictWriter` writes **dictionaries** as CSV rows. You tell it the column names (`fieldnames`), then give it dictionaries whose keys match.

**File:** `logger.py` (add below `needs_header()`)

```python
def save_snapshot(summary):
    """
    Add one row to logs/snapshots.csv using a resource summary dictionary.
    Return the path of the file that was written.
    """

    # Make sure the logs folder exists
    # TODO: Use os.makedirs() to create LOG_FOLDER if it is missing.
    os.__________(LOG_FOLDER, exist_ok=True)

    # Check this BEFORE opening the file (opening creates it)
    # TODO: Call your needs_header() function.
    write_header = ______________________

    row = {
        "timestamp": get_timestamp(),

        # TODO: Copy the values from the summary dictionary.
        "cpu_percent": summary["______________"],
        "memory_percent": ______________________,
        "disk_percent": ______________________,
    }

    # TODO: Open LOG_FILE in append mode.
    with open(LOG_FILE, "___", newline="") as csv_file:
        # TODO: Pass the list of column names as fieldnames.
        writer = csv.DictWriter(csv_file, fieldnames=______________)

        # TODO: Only write the header if the file needed one.
        if ______________:
            writer.writeheader()

        # TODO: Write the row dictionary to the file.
        writer.______________(row)

    # TODO: Return the path of the log file.
    return ______________
```

**Fill-in Hints**

- Useful function: `os.makedirs(path, exist_ok=True)` creates a folder. `exist_ok=True` means "no error if it already exists."
- `needs_header()` returns `True` or `False`. Store that result.
- The summary keys are the same ones from Part 6: `"cpu_percent"`, `"memory_percent"`, `"disk_percent"`.
- Append mode is a single letter (see the table above).
- The column names are stored in the constant `FIELDNAMES`.
- The method that writes one dictionary as a row is `writerow()`.
- `newline=""` is required by the `csv` module to prevent blank lines between rows on Windows. It is already written for you.
- The path constant you are writing to is `LOG_FILE`.

### Step 10.6: Test the logger

Replace everything in `scratch.py` with:

```python
import monitor
import logger

summary = monitor.get_resource_summary()

path = logger.save_snapshot(summary)
print("Saved to:", path)

path = logger.save_snapshot(summary)
print("Saved again to:", path)
```

Run `python scratch.py`.

```text
Saved to: C:\Users\jordan\Documents\tb-system-resource-monitor\logs\snapshots.csv
Saved again to: C:\Users\jordan\Documents\tb-system-resource-monitor\logs\snapshots.csv
```

Now open `logs/snapshots.csv` in VS Code. It should look like:

```text
timestamp,cpu_percent,memory_percent,disk_percent
2026-10-27 18:30:00,32.5,61.7,72.3
2026-10-27 18:30:01,32.5,61.7,72.3
```

**Check:**

- [ ] The header row exists, and appears **only once** (on the first line).
- [ ] Each data row has a timestamp.
- [ ] Each data row has a CPU value, a memory value, and a disk value.
- [ ] Running the test again **adds** rows instead of replacing them.
- [ ] `git status` does **not** list `snapshots.csv` (your `.gitignore` is working).

To start fresh, you can delete `snapshots.csv`. The logger will create it again, with a new header, the next time.

### Git Checkpoint 8

```bash
git status
git add .
git commit -m "Add CSV snapshot logger"
git push
```

---

## Part 11: Build the Main Menu

Everything works on its own. Now you will connect it all with a menu in `main.py`, the file the user actually runs.

### Step 11.1: Start `main.py`

**File:** `main.py`

```python
"""
main.py

Menu and user interaction for the TB System Resource Monitor.
Run this file to start the program:

    python main.py
"""

# TODO: Import your two modules: monitor and logger.
import ______________
import ______________
```

**Fill-in Hints**

- Import your own modules by their file names **without** `.py`.

### Step 11.2: Write `print_menu()` and `pause()`

**File:** `main.py` (add below the imports)

```python
def print_menu():
    """
    Print the main menu.
    """

    print()
    print("=" * 32)
    print("    TB System Resource Monitor")
    print("=" * 32)
    print("1. View Current System Status")
    print("2. Start Live Monitor")
    print("3. View Top Processes")
    print("4. Save Current Snapshot")

    # TODO: Print the last two menu options (5 and 6).
    print("5. ______________________________")
    print("6. ______")
    print("=" * 32)


def pause():
    """
    Wait for the user to press Enter before showing the menu again.
    """

    input("\nPress Enter to return to the menu...")
```

**Fill-in Hints**

- Look at the menu in Step 1.1 for the exact wording of options 5 and 6.
- `input()` waits for the user to type something and press Enter. Here, we do not need what they typed; we just use it to pause so the user can read the results before the menu reappears.
- `\n` inside a string means "new line."

### Step 11.3: Write `view_current_status()`

**File:** `main.py` (add below `pause()`)

When you use a function from another module, you write `module_name.function_name()`, for example `monitor.get_cpu_usage()`.

```python
def view_current_status():
    """
    Menu option 1: show the current status and any warnings.
    """

    print("\nGathering system information...")

    # TODO: Get a resource summary from the monitor module.
    summary = monitor.______________________()

    # TODO: Display the summary, then display any warnings.
    monitor.______________________(summary)
    print()
    monitor.______________________(summary)
```

**Fill-in Hints**

- Functions you built in `monitor.py`: `get_resource_summary()`, `display_resource_summary()`, `display_warnings()`.
- The "Gathering..." message is there because getting the summary takes about 1 second. It tells the user the program is working.

### Step 11.4: Write `save_current_snapshot()`

Saving a file can fail. For example, on Windows, if `snapshots.csv` is open in Excel, Excel locks it and Python cannot write to it. Python raises an **`OSError`** (a general "operating system / file" error). You will catch it and show a friendly message.

**File:** `main.py` (add below `view_current_status()`)

```python
def save_current_snapshot():
    """
    Menu option 4: save the current status to the CSV log.
    """

    print("\nGathering system information...")

    summary = monitor.get_resource_summary()

    try:
        # TODO: Save the summary using the logger module.
        file_path = logger.______________________(summary)
        print(f"Snapshot saved to: {file_path}")

    # TODO: Catch the general file error described above.
    except ______________:
        print("Sorry, the snapshot could not be saved.")
        print("Make sure the CSV file is not open in another program.")
```

**Fill-in Hints**

- The function you built in `logger.py` is `save_snapshot()`.
- The exception name is in the paragraph above the code.

### Step 11.5: Write the menu loop in `main()`

The menu should keep showing until the user picks **Exit**. That is a `while True:` loop that only stops when you use **`break`**, which immediately exits the loop.

`input()` always returns **text** (a string), so compare the choice to strings like `"1"`, not numbers like `1`. `.strip()` removes extra spaces, so `" 1 "` becomes `"1"`.

**File:** `main.py` (add below `save_current_snapshot()`)

```python
def main():
    """
    Run the menu loop until the user chooses Exit.
    """

    while True:
        print_menu()
        choice = input("Choose an option (1-6): ").strip()

        if choice == "1":
            view_current_status()
            pause()

        # TODO: Option 2 starts the live monitor.
        elif choice == "___":
            monitor.______________________()
            pause()

        # TODO: Option 3 shows the top processes.
        elif choice == "3":
            monitor.______________________()
            pause()

        # TODO: Option 4 saves a snapshot (use your function from Step 11.4).
        elif choice == "4":
            ______________________()
            pause()

        # TODO: Option 5 shows the system information.
        elif choice == "___":
            monitor.______________________()
            pause()

        # TODO: Option 6 says goodbye and exits the loop.
        elif choice == "6":
            print("Goodbye!")
            __________

        # TODO: Anything else is an invalid choice.
        __________:
            print("Invalid choice. Please enter a number from 1 to 6.")
```

**Fill-in Hints**

- Monitor functions: `start_live_monitor()`, `display_top_processes()`, `display_system_info()`.
- Option 4 calls `save_current_snapshot()`, which lives in `main.py` itself, so there is **no** `monitor.` in front.
- The keyword that exits a loop is `break`.
- The final catch-all branch of an `if`/`elif` chain is `else` (it has no condition).
- **Why does an invalid choice not crash?** Because the `else` branch handles *any* text that is not `"1"` to `"6"`, including letters or an empty answer. The loop then shows the menu again.

### Step 11.6: Start the program

**File:** `main.py` (add at the very bottom, with **no** indentation)

```python
if __name__ == "__main__":
    try:
        # TODO: Call the main() function.
        ______________

    # TODO: Catch Ctrl+C (KeyboardInterrupt) and end-of-input (EOFError).
    except (______________________, EOFError):
        print("\nGoodbye!")
```

**Fill-in Hints**

- `if __name__ == "__main__":` means "only run this when this file is run directly" (`python main.py`), not when it is imported by another file. This is a standard Python pattern.
- You learned the name of the `Ctrl+C` exception in Part 8. Catching it here means pressing `Ctrl+C` at the menu exits cleanly instead of showing a traceback.
- `EOFError` happens if the input stream closes (for example, `Ctrl+D` on macOS/Linux or `Ctrl+Z` then Enter on Windows). It is already filled in for you.

### Step 11.7: Run the full program

From now on, you run the real program instead of `scratch.py`:

```bash
python main.py
```

You should see the menu. Try option **5** first (it is the quickest), press Enter, then try option **6** to exit.

### Git Checkpoint 9

```bash
git add .
git commit -m "Add main menu and connect all features"
git push
```

---

## Part 12: Test the Complete Project

Now test every feature through the menu, the way a real user would. Run:

```bash
python main.py
```

### Step 12.1: Menu tests

| # | Test | What to type | Expected result | Pass? |
|---|---|---|---|---|
| 1 | Current status | `1` | "Gathering..." then CPU, memory, disk with 2-decimal GB values, then "All resources are within normal limits." (or real warnings) | [ ] |
| 2 | Live monitor | `2` | Screen refreshes every few seconds with changing CPU values | [ ] |
| 3 | Stop live monitor | `Ctrl+C` during the live monitor | "Live monitor stopped..." then "Press Enter to return to the menu..." with **no** traceback | [ ] |
| 4 | Top processes | `3` | Table of 5 processes, highest memory first | [ ] |
| 5 | Save snapshot | `4` | "Snapshot saved to: ...snapshots.csv" | [ ] |
| 6 | System info | `5` | OS, computer name, processor, Python version | [ ] |
| 7 | Invalid number | `9` | "Invalid choice. Please enter a number from 1 to 6." then the menu again | [ ] |
| 8 | Invalid text | `hello` | Same friendly invalid message | [ ] |
| 9 | Empty input | Just press Enter | Same friendly invalid message | [ ] |
| 10 | Exit | `6` | "Goodbye!" and the program ends | [ ] |
| 11 | Ctrl+C at menu | `Ctrl+C` at the "Choose an option" prompt | "Goodbye!" with **no** traceback | [ ] |

### Step 12.2: Logger test through the menu

1. Choose option **4** two or three times.
2. Exit and open `logs/snapshots.csv`.
3. Confirm:
   - [ ] The header `timestamp,cpu_percent,memory_percent,disk_percent` appears once, on line 1.
   - [ ] One new row was added for each time you chose option 4.
   - [ ] Every row has a timestamp, CPU value, memory value, and disk value.

### Step 12.3: Run from a different folder (optional but recommended)

In the terminal, move up one folder and run the program using its path:

```bash
cd ..
python tb-system-resource-monitor/main.py
```

Save a snapshot. It should still go into `tb-system-resource-monitor/logs/`, because `logger.py` builds the path from its own location. Then go back:

```bash
cd tb-system-resource-monitor
```

### Step 12.4: Final code review

Before moving on, check your code:

- [ ] No `____` blanks or `TODO` placeholders are left that should have been replaced. (You may delete the `# TODO` comment lines now, or keep them as notes.)
- [ ] Thresholds are back to `80`, `80`, `90`.
- [ ] `REFRESH_SECONDS` is `2`.
- [ ] You can explain, in your own words, what each function does.

### Git Checkpoint 10

```bash
git add .
git commit -m "Complete testing and code cleanup"
git push
```

---

## Part 13: Write Your README and Submit

### Step 13.1: Why your README matters

Your `README.md` is the first thing anyone sees on your GitHub repository, including recruiters. A clear README turns "some code" into a **portfolio project**. Write it for someone who has never heard of Trailblazers.

**Do not copy the Trailblazers assignment README.** Write your own, describing *your* version of the project.

### Step 13.2: Write your personal README

**File:** `README.md` (the one GitHub created in Part 2). Replace its contents with your own README that includes **all** of these sections:

1. **Project title**: for example, `# TB System Resource Monitor`
2. **What the application does**: 2-4 sentences in your own words.
3. **Features**: a bullet list of what it can do.
4. **Technologies**: Python, psutil, and the standard-library modules you used.
5. **Project structure**: the file tree with a one-line description of each file.
6. **Installation**: how to clone the repo and install requirements, for example:

   ```bash
   git clone https://github.com/YOUR-USERNAME/tb-system-resource-monitor.git
   cd tb-system-resource-monitor
   python -m pip install -r requirements.txt
   ```

7. **How to run**: for example, `python main.py`.
8. **Menu options**: what each of the 6 options does.
9. **Screenshots / demo**: at least one screenshot of your program running (see Step 13.3).
10. **Known limitations**: be honest. Ideas: CPU measurement adds a 1-second delay; some processes cannot be read without administrator access; only the main disk is measured; memory "used" is calculated differently on macOS.
11. **Optional features I added**: list any extensions from Part 15 (or write "None yet").
12. **What I learned**: a few sentences about the skills you practiced.

**Markdown basics** (the formatting language README files use):

```markdown
# Big heading
## Smaller heading
- Bullet point
**bold text**
`inline code`
![Screenshot description](screenshots/menu.png)
```

### Step 13.3: Add a screenshot

1. Run `python main.py` and take a screenshot of the menu or the live monitor.
   - Windows: `Win+Shift+S`
   - macOS: `Cmd+Shift+4`
   - Linux: usually `PrtSc` or the Screenshot app
2. Create a folder named `screenshots` in your project and save the image there (for example, `screenshots/live-monitor.png`).
3. Add it to your README:

   ```markdown
   ![Live monitor running](screenshots/live-monitor.png)
   ```

> Check that your screenshot does not show anything private (other windows, personal files, etc.).

### Git Checkpoint 11

```bash
git add .
git commit -m "Write project README with screenshots"
git push
```

Open your repository on GitHub and confirm your README displays correctly with the screenshot.

> **When do I use `git pull`?** If you ever edit a file directly on the GitHub website (like fixing a typo in your README there), your computer will not have that change. Run `git pull` in VS Code before working again so your local copy is up to date. If `git push` is ever rejected with a message about "fetch first," run `git pull` and then push again.

### Step 13.4: Submit your project

Your project is complete in your personal repository. To submit it to Trailblazers, follow the instructions in the central Trailblazers repository:

**[Submissions/README.md](./Submissions/README.md)**

Those instructions explain how to fork the central TB repository and submit your project through a pull request. Do not skip any steps there.

---

## Part 14: Troubleshooting

### "NameError: name '____' is not defined"

You left a blank in your code. In Python, `____` is actually a valid variable name, so Python tries to look it up and fails. Search your file for `__` (use `Ctrl+F` / `Cmd+F`) and fill in every blank. The error message shows the file and line number.

### "ModuleNotFoundError: No module named 'psutil'"

psutil is not installed for the Python you are using.

1. Install it with the same command you use to run your program:
   - If you run `python main.py`, install with `python -m pip install psutil`.
   - If you run `py main.py`, install with `py -m pip install psutil`.
   - If you run `python3 main.py`, install with `python3 -m pip install psutil`.
2. In VS Code, run **Python: Select Interpreter** and pick the same Python.
3. If you use the VS Code "Run" (play) button, it might use a different Python than your terminal. Running from the terminal is more predictable.

### "ModuleNotFoundError: No module named 'monitor'"

- Make sure `monitor.py` is spelled correctly and is in the **same folder** as the file importing it.
- Make sure your terminal is in the project folder (run `cd tb-system-resource-monitor` if needed).

### "error: externally-managed-environment" (macOS / Linux)

Some newer macOS (Homebrew) and Linux systems block installing packages directly. Create a **virtual environment**, a private Python setup for this project:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

You will see `(.venv)` in your terminal prompt. Run `source .venv/bin/activate` again each time you open a new terminal. Your `.gitignore` already ignores the `.venv/` folder. In VS Code, select the `.venv` Python with **Python: Select Interpreter**.

### Windows: typing `python` opens the Microsoft Store

Windows has a placeholder `python` command. Either use `py` instead, or install Python from python.org with **"Add python.exe to PATH"** checked, then restart VS Code.

### "IndentationError" or "unexpected indent"

Python uses indentation (spaces at the start of a line) to group code. Code inside a function, `if`, `for`, `while`, `try`, or `with` must be indented one level more (4 spaces) than the line above it ending in `:`. Make sure you did not mix tabs and spaces. VS Code's default of 4 spaces is correct.

### "SyntaxError: invalid syntax"

Check the line mentioned and the line **above** it for:

- A missing `:` at the end of a `def`, `if`, `elif`, `else`, `for`, `while`, `try`, `except`, or `with` line.
- A missing closing `)`, `]`, `}`, or quotation mark.
- A missing comma between dictionary items.

### "KeyError: 'something'"

You used a dictionary key that does not exist. Check the spelling against where the dictionary was created. Keys are case-sensitive: `"cpu_percent"` and `"CPU_percent"` are different.

### "TypeError: ... object is not callable" or strange output like `<function ...>`

- `<function get_cpu_usage at 0x...>` printed instead of a number means you forgot the `()` when calling a function.
- `'int' object is not callable` near `process.pid` means you wrote `process.pid()`. `pid` is an attribute, so it has no parentheses.

### CPU usage always shows 0.0

- Make sure you used `interval=1`. Without an interval, the first call returns `0.0`.
- On a very idle computer, low values are normal. Open a video or a few programs and try again.

### Disk usage looks wrong on macOS

If "Used Disk" is very small (like 10-15 GB) on macOS, check that `get_disk_path()` includes the `"Darwin"` branch. Modern macOS stores your files on the `/System/Volumes/Data` volume, not `/`.

### Live monitor does not clear the screen

- Make sure `clear_screen()` is called inside the loop.
- Some VS Code output panels (like the "Run" button's Output tab) do not support clearing. Run the program in the **Terminal** with `python main.py`.

### Ctrl+C shows a long traceback

- Check that your `except` says `KeyboardInterrupt` exactly (capital K and I).
- Make sure the entire `while` loop is **indented inside** the `try:` block.

### The CSV has blank lines between rows (Windows)

Make sure `newline=""` is in your `open()` call.

### "PermissionError" when saving a snapshot

The CSV file is probably open in Excel or another program that locked it. Close it and try again. Your `try/except OSError` should show the friendly message instead of crashing.

### `git push` asks for a password, or is rejected

- GitHub does not accept your account password in the terminal. Let VS Code sign you in, or follow the browser sign-in prompt from Git Credential Manager.
- If the push is rejected with "fetch first" or "non-fast-forward," run `git pull`, then `git push` again.

### I accidentally named a file `psutil.py`, `csv.py`, `time.py`, or `platform.py`

Do not name your files the same as modules you import. Python will import **your** file instead of the real module. Rename your file, and delete any `__pycache__` folder.

---

## Part 15: Optional Extensions

> **OPTIONAL.** Only start these **after** the required project is finished, tested, and pushed. None of these are required for your submission. If you add any, describe them in your README's "Optional features I added" section, and commit each one separately.

Ideas, roughly from easier to harder:

| Extension | Idea | Hint |
|---|---|---|
| System uptime | Show how long the computer has been on | `psutil.boot_time()` and `time.time()` |
| CPU-per-core display | Show usage for each CPU core | `psutil.cpu_percent(interval=1, percpu=True)` returns a list |
| Configurable thresholds | Let the user change warning limits from the menu | Update the `THRESHOLDS` dictionary using `input()`; validate with `try/except ValueError` |
| Search/filter processes | Find processes whose name contains a word | Loop over processes and use `in` with `.lower()` |
| Repeated logging | Save a snapshot every X seconds | A `while` loop with `time.sleep()` that calls `save_snapshot()`; stop with `Ctrl+C` |
| Historical logging | Show the last 10 snapshots from the CSV | `csv.DictReader` |
| Exporting reports | Write a readable `.txt` report of the current status | `open(path, "w")` and `file.write()` |
| Network usage | Show data uploaded/downloaded | `psutil.net_io_counters()` (`bytes_sent`, `bytes_recv`) |
| Battery monitoring | Show battery percent on laptops | `psutil.sensors_battery()` (returns `None` on desktops; handle that) |
| CPU-per-process | Add a CPU column to top processes | `process.cpu_percent()` must be called twice with a pause in between; read the psutil docs |
| Charts/graphs | Graph CPU/memory over time from your CSV | `matplotlib` (add it to `requirements.txt` if you use it) |
| Tkinter GUI | A window with labels that update | `tkinter` (built in) and `.after()` for refreshing |
| Dashboard | A full-screen live dashboard combining everything | Combine the live monitor, top processes, and network usage |

**Do not** add features that kill processes, change process priorities, or require administrator access.

psutil documentation: https://psutil.readthedocs.io

---

## Final Knowledge Check

You should be able to answer these questions in your own words. You may be asked about them when you present your project.

1. What is CPU usage?
2. What is RAM?
3. What does disk usage represent?
4. What is `psutil`?
5. What is a Python module?
6. What is a function?
7. Why do functions return values?
8. What is a dictionary?
9. Why did we use dictionaries in this project?
10. What does a `for` loop do?
11. What does a `while` loop do?
12. What does `try/except` do?
13. Why can reading process information sometimes fail?
14. What does sorting the process list accomplish?
15. What is CSV?
16. Why do we use timestamps in logs?
17. What is the difference between a Git commit and a Git push?
18. What does cloning a repository mean?
19. How does the live monitor keep updating?
20. What part of the project would you improve next?

**Bonus questions:**

21. Why does `get_cpu_usage()` take about 1 second to run?
22. Why does `logger.py` open the CSV file in `"a"` mode instead of `"w"` mode?
23. Why are the CSV log files ignored by Git, but the `logs/` folder is kept?
24. Why does the menu compare `choice` to `"1"` instead of `1`?

---

**Congratulations!** You built a working, cross-platform system monitor in Python and published it on GitHub. That is a real portfolio project.