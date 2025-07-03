---
layout: guide
title: "05 Adversary Tactics and Threat Intelligence"
---

### An Introduction to Thinking Like the Enemy

This guide elevates your perspective from a hands-on tool user to a strategic thinker. You'll learn about the frameworks used to describe and categorize attacker behavior and how to use public threat intelligence to enrich your understanding of a potential threat.

---

## Part 1: The MITRE ATT&CK® Framework

**Goal:** To understand the industry-standard language for describing how adversaries operate.

### Key Concepts (The Theory)

- **MITRE ATT&CK®:** This is a globally accessible knowledge base of adversary tactics and techniques based on real-world observations. Think of it as a comprehensive "encyclopedia of bad guy behavior." It is not a tool or a piece of software, but a reference framework used by security professionals worldwide.
- **Tactics:** These represent the "why" or the technical goal of an attacker. They are the columns across the top of the ATT&CK matrix (e.g., `Initial Access`, `Execution`, `Persistence`, `Exfiltration`).
- **Techniques:** These represent the "how" an adversary achieves a tactic. Each tactic has multiple techniques listed under it. For example, under the `Initial Access` tactic, one common technique is `Phishing`.

### Practical Exercises (Hands-On Labs)

1.  **Explore the ATT&CK Matrix:**
    - Open the **[MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)**.
    - Take a moment to look it over. The layout can be intimidating at first, but the logic is straightforward. Read the column headers from left to right to see a logical flow that an attack could follow.
    - Click on the **`Persistence`** tactic column header. This will open a page describing the attacker's goal: to maintain their foothold on a system.
    - Now go back to the matrix and click on a specific technique under `Persistence`, such as **`Create Account`**. Read the description. You'll see an explanation of how attackers create new accounts on a system to ensure they can get back in later. You'll also see real-world examples of threat groups that use this specific technique.

---

## Part 2: The Pyramid of Pain

**Goal:** To understand why some types of threat indicators are more valuable to a defender than others.

### Key Concepts (The Theory)

- **Indicator of Compromise (IOC):** An IOC is a piece of digital evidence that points to a potential intrusion. An IP address, a domain name, or a file hash are all examples of IOCs.
- **The Pyramid of Pain:** This is a conceptual model that organizes different types of IOCs into a pyramid. The idea is simple: the higher you go up the pyramid, the more "pain" you cause the adversary when you deny them that indicator. Blocking a simple file hash is easy for them to overcome (they can just change one bit in the file), but forcing them to change their core Tactics, Techniques, and Procedures (TTPs) is very difficult and costly for them.

  - **Trivial (Bottom):** Hash Values, IP Addresses, Domain Names
  - **Challenging:** Network/Host Artifacts
  - **Tough (Top):** Tools, TTPs

### Practical Exercises (Hands-On Labs)

1.  **A Thought Experiment:**
    - Imagine you are defending against an attacker. You discover a piece of their malware and block its MD5 hash value in your security tools. The next day, they attack again with a new version of the malware that has a completely different hash. This was easy for them.
    - Now, imagine you analyze the malware and discover the _technique_ it uses to achieve persistence (e.g., creating a Scheduled Task). You then create a security rule to monitor for _any_ program that uses that specific technique in an unusual way.
    - Now, to get around your defense, the attacker has to completely redesign their tool. This causes them much more "pain" and is a more durable defense. That is the principle of the Pyramid of Pain in action.

---

## Part 3: Practical Threat Intelligence

**Goal:** To use public threat intelligence platforms to enrich your knowledge about a specific threat indicator.

### Key Concepts (The Theory)

- **Threat Intelligence:** This is contextual information about threats and adversaries that helps organizations protect themselves. It's about moving from a simple alert (e.g., "Connection to IP 1.2.3.4") to an informed assessment ("Connection to IP 1.2.3.4, which is a known command-and-control server for the 'EvilScorpion' malware family").

### Practical Exercises (Hands-On Labs)

1.  **Research a Malicious Indicator:**

    - Let's find a recently reported, live threat indicator. A great source for this is **[ThreatFox by abuse.ch](https://threatfox.abuse.ch/browse/)**. This site lists malware indicators shared by the security community in the last 24 hours.
    - Open the ThreatFox link. You will see a list of recent IOCs (hashes, IPs, URLs).
    - Pick an IP address from the list. **Do not browse to it or interact with it in any way.**

2.  **Enrich the Indicator with VirusTotal:**
    - Copy the malicious IP address you chose.
    - Go to **[VirusTotal](https://www.virustotal.com/)**, click on the **Search** tab (it can search for IPs, domains, hashes, etc.).
    - Paste the IP address and press Enter.
    - Look at the results. You will see not only how many vendors flag it as malicious, but you can also click on the **Community** tab. In the community section, you will often find comments from other security researchers providing context, such as what malware family the IP is associated with or what phishing campaign it belongs to. This process of taking one piece of data and learning more about it from other sources is called "enrichment," and it is a fundamental task for a SOC analyst.
