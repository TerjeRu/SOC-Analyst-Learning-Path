---
layout: guide
title: "06 The Anatomy of an Investigation"
---

### A Framework for Handling Security Alerts

This guide provides a structured framework for responding to a security alert. Knowing how to use tools is important, but using them within a repeatable, logical process is what separates a beginner from a professional analyst. This workflow ensures that your investigations are thorough, consistent, and easy for your teammates to understand.

---

## Part 1: The Alert – Triage and Prioritization

**Goal:** To learn how to perform "triage" on incoming alerts to quickly assess their importance and decide what to work on first.

### Key Concepts (The Theory)

- **Triage:** Just like in a hospital emergency room, security triage is the process of sorting new alerts based on their urgency and severity. This ensures that the most critical threats are handled first.
- **Alert Fidelity:** This refers to the trustworthiness of an alert source. A "high-fidelity" alert (e.g., an EDR alert for known malware) is very likely to be a real problem. A "low-fidelity" alert (e.g., a user logging in from a new location) might be interesting, but could also be normal behavior.
- **Severity vs. Priority:**
  - **Severity** is how bad the event _could_ be (e.g., High, Medium, Low).
  - **Priority** is the order in which _you_ should handle it. A medium-severity alert on a critical server might be a higher priority than a high-severity alert on a test machine.

### The Initial Triage Checklist

When a new alert comes in, mentally run through these questions:

1.  **What is the alert?** (e.g., Malware detected, Impossible travel, Phishing email reported).
2.  **What is the assigned severity?** (High, Medium, Low).
3.  **What is the asset?** Is it a critical server, a standard user's laptop, a developer's machine?
4.  **Who is the user?** Are they a standard user, an executive (VIP), or an administrator with elevated privileges?

Answering these helps you decide if this is something you need to drop everything for, or if it can be investigated in a more routine manner.

---

## Part 2: The Investigation Loop (OODA)

**Goal:** To use a simple, memorable loop to structure your active investigation.

### Key Concepts (The Theory)

The **OODA Loop** (Observe, Orient, Decide, Act) is a four-step model that is perfect for security investigations.

1.  **Observe:** Gather the raw facts without judgment. Collect all the IOCs (Indicators of Compromise) and data points from the alert. This is the "what" phase.

    - _Examples:_ Usernames, hostnames, IP addresses, file hashes, process names, command-line arguments, timestamps.

2.  **Orient:** This is the most important step. You take the raw data you observed and give it context. This is where you use your tools and knowledge to figure out what the data _means_.

    - _Examples:_ Look up the IP address on VirusTotal, check the file hash against threat intelligence, review the user's recent activity, see if the process behavior is normal for that machine, reference the MITRE ATT&CK framework.

3.  **Decide:** Form a hypothesis. Based on your orientation, you decide what you think is happening. The most common conclusions are:

    - **True Positive:** This is a real, malicious event. The alert is correct.
    - **False Positive:** The alert fired on benign activity. It is not a threat.
    - **Benign True Positive:** The alert is technically correct, but the activity is not malicious (e.g., an administrator using a tool that looks like hacking software).

4.  **Act:** Based on your decision, you take an action.
    - _Examples:_ Isolate the host from the network, block the IP address at the firewall, delete the malicious email, close the alert as a false positive, or escalate to a senior analyst.

After you act, the loop repeats. Your action may generate new information, so you observe it, orient yourself to the new situation, and continue.

---

## Part 3: Documentation and Escalation

**Goal:** To understand the importance of good note-keeping and know when to ask for help.

### Key Concepts (The Theory)

Good documentation is not optional. It is essential for teamwork, for tracking your own work, and for creating a historical record that can be used to identify trends. Every action you take should be documented in the ticket or case file.

### A Simple Note-Taking Framework

When updating a ticket, make sure your notes are clear and concise. A good summary should include:

- **Summary:** What was the alert about in one sentence? (e.g., "High-severity alert for malware execution on host SRV-01.")
- **Investigation:** What were the key things you found? (e.g., "Confirmed process `evil.exe` connected to malicious IP 1.2.3.4. VirusTotal confirms this IP is a C2 server for TrickBot.")
- **Action Taken:** What did you do? (e.g., "Isolated host SRV-01 from the network via Defender. Escalated to the Tier 2 team for remediation.")
- **Next Steps:** What still needs to be done? (e.g., "Awaiting confirmation from Tier 2 that the host has been cleaned.")

### When to Escalate

Knowing when to ask for help is a sign of strength, not weakness. Escalate to a senior analyst or manager if:

- You have confirmed a critical, active threat (a "True Positive").
- The alert involves a VIP user or a critical system.
- You are about to take a significant action you are unsure about (e.g., shutting down a production server).
- You have spent a reasonable amount of time on an investigation and are stuck. Don't be afraid to ask for a second opinion.
