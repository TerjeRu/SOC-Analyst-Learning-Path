---
layout: guide
title: "02 Cybersecurity Investigator Tools"
---

### An Introduction to Digital Investigation

This guide builds on the foundations from the first session, moving you from understanding concepts to actively investigating digital activity. You'll learn to use standard, free tools to analyze network traffic, inspect websites, and examine potentially suspicious files.

---

## Part 1: Intercepting Network Traffic

**Goal:** To capture and analyze your own network traffic, seeing the raw data behind your internet activity.

### Key Concepts (The Theory)

- **Packet Capture (PCAP):** This is the act of recording all the data packets that cross a network interface, much like wiretapping your own internet connection. The file containing this data is often called a PCAP file.
- **Wireshark:** The world's most popular network protocol analyzer. It's a free, industry-standard tool that lets you view the contents of a PCAP file in a human-readable format.
- **The Three-Way Handshake:** TCP connections, used for most web traffic, begin with a three-step process: SYN (synchronize), SYN-ACK (synchronize-acknowledge), and ACK (acknowledge). Seeing this pattern confirms a stable connection was established.
- **HTTP vs. HTTPS:** With HTTP, your Browse traffic is in plain text. With HTTPS, that traffic is encrypted. In Wireshark, you can read the contents of HTTP traffic, but HTTPS data will appear as scrambled, unreadable text.

### Practical Exercises (Hands-On Labs)

1.  **Install Wireshark**

    - Download and install **[Wireshark](https://www.wireshark.org/download.html)**. Accept the default installation options. On Windows, this will also install `Npcap`; this is required and safe.

2.  **Capture Your Network Traffic**

    - Open Wireshark. You will see a list of network interfaces.
    - Double-click on the interface that shows activity (a moving sparkline). This is your active connection, and the capture will begin immediately.
    - Open your web browser and visit **[http://neverssl.com](http://neverssl.com)** (this site intentionally uses HTTP so you can see unencrypted traffic).
    - Go back to Wireshark and click the red "Stop" button in the toolbar.

3.  **Analyze the Capture**
    - In the "Apply a display filter" bar at the top, type `http` and press Enter. This filters the capture to show only HTTP traffic.
    - Look for a packet in the "Info" column that says `GET /`. This is your browser's request to get the main webpage.
    - Right-click on that `GET` packet and choose **Follow > TCP Stream**. A new window will pop up showing you the raw HTML of the website you visited. You are reading the actual data that was sent to your browser.

---

## Part 2: Inspecting Web Activity

**Goal:** To analyze the components of a website and examine online threats using web-based tools.

### Key Concepts (The Theory)

- **Browser Developer Tools:** Every modern browser has built-in tools that are incredibly useful for security analysis. The "Network" tab shows every request a webpage makes, and the "Inspector" or "Elements" tab shows the page's source code.
- **URL Analysis:** Not all links are what they seem. A key skill is dissecting a URL to spot suspicious parts, like strange subdomains (`secure.paypal.com.evilsite.net`) or attempts to hide the true file type (`document.pdf.exe`).
- **Online Sandboxing:** A sandbox is a secure, isolated environment where you can safely open a suspicious link or file to see what it does without infecting your own computer. Services like VirusTotal are critical tools for analysts.

### Practical Exercises (Hands-On Labs)

1.  **Inspect a Website with Developer Tools**

    - Go to any news website.
    - Right-click anywhere on the page and select **Inspect**.
    - Click on the **Network** tab in the developer tools panel.
    - Refresh the webpage. Watch as the Network tab populates with dozens or even hundreds of requests, showing you how a single webpage is actually composed of many different files and requests to other servers.

2.  **Analyze a Suspicious Link with VirusTotal**
    - **[VirusTotal](https://www.virustotal.com)** is a free service that analyzes files and URLs with dozens of different antivirus engines.
    - Find a suspicious link. You can go back to **[PhishTank](https://phishtank.org/)** to find one. **Right-click** on a link from the list and **Copy Link Address**. **DO NOT VISIT THE SITE.**
    - On the VirusTotal website, click the **URL** tab, paste the suspicious link, and press Enter.
    - Examine the results to see how many different security vendors flagged the link as malicious.

---

## Part 3: Examining Logs and Endpoints

**Goal:** To understand the basics of log analysis and the principles of endpoint detection.

### Key Concepts (The Theory)

- **Log Files:** Every operating system and application generates logs, which are timestamped records of events (e.g., a user logging in, a program starting). For an analyst, logs provide the digital breadcrumbs needed to trace an attacker's steps.
- **Correlation:** The real power of log analysis comes from _correlating_ events across different log sources. Seeing a firewall block a connection from a known bad IP at the same time a user's machine tries to connect to that IP is a strong indicator of compromise.

### Practical Exercises (Hands-On Labs)

1.  **Explore Local System Logs**

    - **On Windows:**

      1.  Open the **Event Viewer** app.
      2.  In the left pane, expand **Windows Logs** and click on **System** or **Security**.
      3.  Browse the events. Note the sheer volume of logged activity. You can use the "Filter Current Log..." action on the right to search for specific events, which is a core task for a Windows administrator or analyst.

    - **On Mac:**
      1.  Open the **Console** app (use Spotlight search with `Cmd + Space`).
      2.  The Console app provides a real-time stream of your system's log files.
      3.  Use the search bar at the top to filter the messages for a specific process (e.g., `kernel`). This demonstrates the first step of log analysis: filtering noise to find specific events.

2.  **Think Like a Log Analyst (A Thought Experiment)**
    - **Scenario:** You are reviewing web server logs. You see a series of 50 failed login attempts for the "admin" account from a single IP address. This is immediately followed by one successful "admin" login from that same IP.
    - **Your thought process:**
      - **What it is:** This pattern strongly suggests a **Brute Force Attack**, where an attacker used automation to guess a password repeatedly.
      - **Next Step:** The immediate priority is containment. You would lock the compromised "admin" account and block the attacker's IP address at the firewall. Afterward, the deeper investigation would begin to determine what the attacker did after gaining access.
