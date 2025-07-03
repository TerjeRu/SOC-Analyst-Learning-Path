---
layout: guide
title: "07 Introduction to SIEM and SOAR"
---

### A Foundation for Modern Security Platforms

This guide explains the core concepts behind the tools used in a modern Security Operations Center (SOC). Understanding the theory of SIEM (Security Information and Event Management) and SOAR (Security Orchestration, Automation, and Response) is essential for working with modern security platforms, as most are built around these core principles.

---

## Part 1: What is a SIEM?

**Goal:** To understand the role of a SIEM as the central "brain" for security data.

### Key Concepts (The Theory)

- **SIEM (Security Information and Event Management):** A SIEM is a system that collects, normalizes, and stores security-related log data from across an entire organization. Think of it as the ultimate library for all your security events.

The three core jobs of a SIEM are:

1.  **Log Collection:** It pulls in logs from thousands of different sources: laptops, servers, firewalls, cloud services, and applications. Without a SIEM, this data would be scattered everywhere and impossible to manage.
2.  **Normalization:** Every source formats its logs differently. A SIEM "normalizes" this data, translating it into a single, standard format. This is like a librarian ensuring all books are organized using the same system, making them easy to find. This step is critical for being able to search across all data sources at once.
3.  **Search and Correlation:** Once the data is collected and normalized, the SIEM allows analysts to search through it to investigate incidents. It can also automatically correlate events. For example, a SIEM correlation rule might say: "If a user has 10 failed logins (from the server logs) followed by one successful login (server logs) and then immediately tries to connect to a known malicious IP (firewall logs), create a high-priority alert."

**In short: A SIEM is a passive listening and search engine. It gathers all the data and helps you find the needles in the haystack.**

---

## Part 2: What is a SOAR?

**Goal:** To understand how a SOAR platform takes action and automates responses.

### Key Concepts (The Theory)

- **SOAR (Security Orchestration, Automation, and Response):** If a SIEM is the brain that _finds_ the problem, a SOAR is the set of hands that _fixes_ the problem. A SOAR platform connects to all your other security tools (like your EDR, firewall, and email system) and allows you to perform actions automatically.

The three core jobs of a SOAR are:

1.  **Orchestration:** This means connecting different, unrelated tools so they can work together in a single workflow. A SOAR can tell your EDR to isolate a host, then tell your firewall to block an IP, all from one central console.
2.  **Automation:** This is the real power of SOAR. It takes the manual, repetitive tasks that analysts perform and automates them. This frees up human analysts to work on more complex investigations.
3.  **Response:** A SOAR platform is the central place where an analyst manages an incident from start to finish, tracking all actions taken, whether they were automated or manual.

**In short: A SOAR is an active, "doing" platform. It takes alerts and automatically executes a series of actions.**

---

## Part 3: Playbooks, Automation, and Workflows

**Goal:** To understand how SOAR platforms use "playbooks" to standardize and automate incident response.

### Key Concepts (The Theory)

- **Playbook:** A playbook is a predefined, digital workflow that outlines the exact steps to take in response to a specific type of alert. It's like a recipe or a checklist for handling an incident.

**Example: A Phishing Email Playbook**

Imagine a user reports a phishing email. Instead of an analyst manually performing every step, a SOAR playbook could automate the following:

1.  **Trigger:** The playbook starts when a user forwards an email to `phishing@company.com`.
2.  **Step 1 (Automated):** The SOAR automatically extracts the sender's address, links, and attachments from the email.
3.  **Step 2 (Automated):** It checks the sender's reputation, looks up the links and attachment hashes on VirusTotal, and scans the email body for keywords.
4.  **Step 3 (Decision Point):** If the indicators are confirmed to be malicious, the playbook proceeds.
5.  **Step 4 (Automated):** The SOAR connects to the email server and searches all mailboxes for other emails from the same sender or with the same subject line.
6.  **Step 5 (Action):** It "zaps" (soft-deletes) all found emails from every user's inbox.
7.  **Step 6 (Notification):** The SOAR automatically creates a ticket in the case management system with all the information it found and assigns it to an analyst for final review.

Modern security platforms are designed to integrate these SIEM and SOAR capabilities into a single interface. By understanding these underlying concepts, you can quickly grasp how any specific platform works and appreciate why each feature exists. This knowledge provides a solid foundation for mastering any toolset you encounter in a SOC.
