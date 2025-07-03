# 01-Cybersecurity-Foundations

### An Introduction to Your Digital World

This guide is your starting point for exploring the basics of cybersecurity. We'll look at how your computer communicates online and introduce the fundamental concepts of digital threats and defenses. This is all about building a solid foundation of knowledge.

---

## Part 1: Exploring Your Network Connection

**Goal:** To understand your computer's address on the network and see its conversations.

### Key Concepts (The Theory)

* **IP Addresses & Ports:** Think of an IP address as a building's street address and a port number as the specific apartment number inside. For example, `8.8.8.8` is one of Google's public servers (the building), and it "listens" for DNS requests on port `53` (the apartment).
* **TCP vs. UDP:** These are two primary methods for sending data.
    * **TCP (Transmission Control Protocol)** is like a registered letter; it's reliable and confirms delivery, used for things like loading a webpage.
    * **UDP (User Datagram Protocol)** is like a postcard; it's fast and sends data without confirming arrival, ideal for services like live video streaming or online gaming.
* **DNS (Domain Name System):** This is the phonebook of the internet. It translates human-friendly domain names (`google.com`) into computer-friendly IP addresses (`142.250.184.164`). Security analysts constantly review DNS logs to see what websites users—and malware—are attempting to contact.

### Practical Exercises (Hands-On Labs)

1.  **Find Your Local IP Address**

    * **On Windows:**
        1.  Open **Command Prompt** (CMD).
        2.  Type the following command and press Enter:
            ```bash
            ipconfig
            ```
        3.  Look for the line labeled "IPv4 Address."

    * **On Mac:**
        1.  Open the **Terminal** app.
        2.  Type the following command and press Enter. This specifically asks for the IP address of your primary connection (usually Wi-Fi or Ethernet, `en0`).
            ```bash
            ipconfig getifaddr en0
            ```
        3.  The command will return just your IP address.

2.  **See Your Active Connections**

    * In the same terminal window (Command Prompt or Terminal), run the `netstat` (network statistics) command to see all active connections from your computer. The `-n` flag displays raw IP addresses and port numbers, which is faster.
        ```bash
        netstat -n
        ```
    * Look at the `Foreign Address` column to see the IP addresses and port numbers your computer is communicating with.

3.  **Use the Internet's Phonebook (DNS)**

    * Use the `nslookup` command to see DNS in action. Type the following into your terminal:
        ```bash
        nslookup [www.google.com](https://www.google.com)
        ```
    * The output will display the IP address(es) for Google's website. You have just performed a task that your computer does automatically thousands of times a day.

---

## Part 2: Understanding Digital Threats

**Goal:** To learn the fundamental types of cyber threats and how they work.

### Key Concepts (The Theory)

* **Malware (Malicious Software):** A general term for any software designed to cause harm.
    * **Viruses:** Attach themselves to legitimate files and need a human to run the file to spread.
    * **Worms:** Can self-replicate and spread across networks without human help.
    * **Trojans:** Disguise themselves as legitimate software. You run the "free game," but it also installs a backdoor.
    * **Ransomware:** Encrypts your files and demands a payment (a ransom) for the decryption key.
* **Phishing & Social Engineering:** The art of manipulating people. Phishing is the most common form, using fake emails or websites to trick you into giving up your password, credit card info, or other sensitive data.
* **Encryption & Hashing:**
    * **Encryption:** A two-way process where you use a key to scramble data (encrypt) and the same or a different key to unscramble it (decrypt). This protects data in transit (like with HTTPS).
    * **Hashing:** A one-way process that takes an input (like a password) and produces a unique, fixed-length string (the "hash"). You cannot turn the hash back into the original password. Systems store password hashes, not the passwords themselves.

### Practical Exercises (Hands-On Labs)

1.  **Analyze a Phishing Email**

    * Go to a website like [PhishTank](https://phishtank.org/) to see examples of real phishing emails. Do not click any links within the examples.
    * Look for the classic signs of a phish: Is there a sense of urgency ("Your account will be suspended!")? Are there spelling mistakes? If you hover your mouse over the links (without clicking), does the link's destination match what the text says?

2.  **Generate a Hash**

    * Use an online tool like [MD5 Hash Generator](https://www.md5hashgenerator.com/).
    * Type in a simple password like `password123` and see the hash it generates.
    * Now, change it slightly to `Password123` (with a capital P) and notice how the hash is completely different. This demonstrates why hashing is so powerful for verifying integrity.

---

## Part 3: Thinking Like a Defender

**Goal:** To learn the basic structure of a security team and the core concepts of detection and response.

### Key Concepts (The Theory)

* **SOC (Security Operations Center):** The central command for a security team where analysts monitor for threats, investigate alerts, and coordinate the response to incidents.
* **SIEM (Security Information and Event Management):** A foundational tool in a SOC. It acts like a giant search engine for all security-related logs, allowing analysts to search for evidence of an attack.
* **EDR (Endpoint Detection and Response):** Think of this as a security camera for a computer (the "endpoint"). It watches for suspicious processes and network connections and can alert the SOC or even automatically quarantine the computer.
* **The Cyber Kill Chain:** A model that outlines the typical steps of an attack: Reconnaissance -> Weaponization -> Delivery -> Exploitation -> Installation -> Command & Control -> Actions on Objectives. A defender's job is to break this chain at any step.

### Practical Exercises (Hands-On Labs)

1.  **Explore Public Security Feeds**

    * Visit a live cyber attack map to get a feel for the kind of data analysts look at. Some excellent, visually impressive examples are the [Kaspersky Cybermap](https://cybermap.kaspersky.com), [Check Point ThreatMAP](https://threatmap.checkpoint.com), and [Radware's Live Threat Map](https://livethreatmap.radware.com).
    * Watch one of the maps for a few minutes. Note the source and destination countries and the common attack types. This gives you a sense of the global, 24/7 nature of cyber threats.

2.  **Think Like an Analyst (A Thought Experiment)**

    * **Scenario:** Imagine you get an EDR alert: `powershell.exe` on a user's computer just made a network connection to a strange IP address in another country.
    * **Your thought process:** What are the first three questions you should ask?
        1.  **Who is the user?** (Are they a regular employee or a system administrator with higher privileges?)
        2.  **What is the IP address?** (Is it a known malicious address? A quick check on a tool like VirusTotal would be the next step.)
        3.  **What happened right before this?** (Did the user just open an email attachment? Did they download a file from the internet?)
    * Answering these questions is the core of an analyst's investigative process.
