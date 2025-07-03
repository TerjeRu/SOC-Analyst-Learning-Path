# 04-Endpoint-Investigation-Techniques

### An Introduction to Live Investigation

This guide teaches you the fundamentals of "live response"—investigating a running computer. You'll learn how to see what programs are active, what network connections they're making, and how malicious software can try to hide and survive a reboot. This is a core skill for any security or IT professional.

---

## Part 1: Process and Service Analysis

**Goal:** To see every process currently running on your system and learn how to spot potential outliers.

### Key Concepts (The Theory)

* **Process:** A process is simply a program that is currently running. Every application you open, and every background task the operating system runs, creates one or more processes.
* **Process ID (PID):** Each process is assigned a unique number called a Process ID (PID). This number can be used to track a specific process or stop it.
* **What to look for:** Analysts often look for processes with strange or misspelled names (e.g., `svch0st.exe` instead of `svchost.exe`), processes without a clear owner or description, or processes using an unexpectedly high amount of CPU or memory.

### Practical Exercises (Hands-On Labs)

#### **On Windows**

1.  **Using Task Manager (GUI):**
    * Press **Ctrl + Shift + Esc** to open the **Task Manager**.
    * Click on the **Details** tab. This gives you a clean list of all running processes, their PID, status, the user they are running as, and memory usage. Sort by different columns to see what's most active on your system.

2.  **Using Command Prompt (CLI):**
    * Open **Command Prompt**.
    * Type `tasklist` and press Enter. This will show you much of the same information from the Details tab in a command-line format, which is useful for scripting.

#### **On Mac**

1.  **Using Activity Monitor (GUI):**
    * Open **Activity Monitor** (you can find it using Spotlight search with `Cmd + Space`).
    * This tool shows you all running processes. You can filter by CPU, Memory, Network, and other metrics. Double-clicking a process gives you more detailed information, including its Parent Process.

2.  **Using Terminal (CLI):**
    * Open the **Terminal** app.
    * Type `ps -ax` and press Enter. This command lists all running processes (`-a` for all users, `-x` to include processes without a controlling terminal).

---

## Part 2: Investigating Network Connections by Process

**Goal:** To connect a specific network connection to the exact process that created it.

### Practical Exercises (Hands-On Labs)

#### **On Windows**

1.  Open **Resource Monitor** (you can search for it in the Start Menu).
2.  Click on the **Network** tab.
3.  The "TCP Connections" and "Listening Ports" sections will show you a list of all active connections and which process (by Image and PID) is responsible for each one. This is incredibly powerful for identifying which program is talking to a suspicious IP address.

#### **On Mac**

1.  Open the **Terminal** app.
2.  Type the following command and press Enter:
    ```bash
    lsof -i
    ```
3.  The `lsof -i` command lists all open files (`lsof`) that are using the internet (`-i`). The output shows you the **Command** (program name), **PID**, **User**, and the **Node** (the local and foreign network addresses).

---

## Part 3: Finding Persistence Mechanisms

**Goal:** To understand the common places where programs hide to ensure they start automatically when a computer reboots.

### Key Concepts (The Theory)

* **Persistence:** In cybersecurity, this is the technique attackers use to make sure their malicious code survives a system restart. They hide their programs in special startup locations that the operating system checks every time it boots up.

### Practical Exercises (Hands-On Labs)

#### **On Windows**

1.  **Task Manager:** The simplest place to look is the **Startup** tab in **Task Manager**. This shows a list of common programs that are enabled to run on boot.
2.  **Autoruns (Advanced):** For a much deeper look, the industry-standard tool is **[Autoruns for Windows](https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns)** from Microsoft.
    * Download and run the tool (no installation needed).
    * It shows you *every single location* in the system where a program can be set to start automatically—from registry keys to scheduled tasks. The "Logon" tab is a great place to start. Anything highlighted in yellow is an entry where the file was not found (potentially uninstalled software), and anything in red is an entry where the file has no digital signature (which can be suspicious).

#### **On Mac**

1.  **System Settings (GUI):**
    * Open **System Settings** > **General** > **Login Items**.
    * This screen shows you applications that are set to open at login, as well as background applications (`Allow in the Background`). This is the primary place to check for persistence on a Mac.
2.  **Exploring System Folders (Advanced):**
    * Malicious software often places `.plist` files (property list files) in specific system folders to launch automatically. You can look inside these folders using the Finder's **Go > Go to Folder...** menu. The two most common locations are:
        * `/Library/LaunchDaemons`
        * `/Library/LaunchAgents`
    * You should be cautious about deleting files from these locations, but looking inside gives you a sense of the legitimate background services your computer uses.
