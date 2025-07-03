# 03-Microsoft-Defender-Basics

### An Introduction to the Security Portal

This guide introduces you to a common tool used by security teams: the Microsoft Defender portal. We'll cover the core concepts of user risk and how to find and remove malicious emails from your organization, moving from theory to the practical tools that defenders use every day.

---

## Part 1: Understanding At-Risk Users

**Goal:** To understand what "user risk" means in Microsoft Defender and why a user might be flagged as "High" risk.

### Key Concepts (The Theory)

* **User Risk Level:** This is a rating (Low, Medium, or High) that Microsoft Defender assigns to a user account based on its activity. It's a calculated probability that the account has been compromised. In many organizations, security teams have policies that automatically trigger actions when a user's risk hits "High," such as forcing a password reset or blocking their sign-in.
* **Identity Protection:** This is the specific feature within Microsoft Defender that detects and reports on risky user activity. It gathers signals from countless sources to spot behavior that deviates from a user's normal patterns.

### Why Does a User's Risk Level Rise?

A user's risk level can increase for many reasons. While security teams typically only react to "High" risk alerts to avoid fatigue from false positives, understanding the triggers is key. Common reasons for a high-risk alert include:

* **Leaked Credentials:** Defender's threat intelligence constantly scans the dark web and other sources. If a user's corporate email and password are found in a public data breach (e.g., from a breach at another website where they used the same password), their risk level will immediately be elevated.
* **Sign-in from an Anonymous IP Address:** If a user signs in using an anonymizer service like a Tor browser or a known anonymous VPN, it is considered high-risk because this is a common tactic for attackers to hide their location.
* **Impossible Travel:** This is a classic indicator of compromise. If a user logs in from Spain and then, five minutes later, logs in from a location in Russia, this is physically impossible. Defender flags this activity, assuming one of the logins must be fraudulent.
* **Sign-in from a Malicious IP Address:** If a sign-in attempt comes from an IP address that is known to be used by attackers (e.g., a server associated with a botnet), the risk level will be raised.

---

## Part 2: Hunting and Removing Malicious Emails

**Goal:** To understand how security analysts find and remove harmful emails from user inboxes across an entire organization.

### Key Concepts (The Theory)

* **Threat Explorer (or Explorer):** This is a powerful search tool within the Defender portal. It allows an analyst with the right permissions to search all email traffic across the entire company for specific threats. You can hunt for emails by sender, subject line, attachment name, and dozens of other indicators.
* **Zero-Hour Auto Purge (ZAP):** ZAP is a feature in Defender for Office 365 that can automatically remove malicious emails *after* they have been delivered. Sometimes, an email seems safe at first but is later identified as phishing or malware. ZAP goes back into user inboxes and "zaps" (quarantines or deletes) the email, even if the user has already read it.
* **Manual Remediation:** While ZAP is automatic, analysts often perform manual "zaps." If a new phishing campaign is discovered, an analyst uses Threat Explorer to find all emails related to that campaign and then triggers an action to pull them from all user inboxes at once.

### The Process of "Hunting and Zapping"

Here’s a simplified version of how an analyst would handle a reported phishing email.

1.  **Get an Indicator:** The process starts with a clue. A user might report a suspicious email, or an automated alert might flag a new threat. The analyst identifies key features, like the email's subject line or the sender's address.
2.  **Hunt in Threat Explorer:** The analyst goes to **Threat Explorer** in the Defender portal. They use the unique details from the suspicious email to create a search query. For example, they might search for all emails received in the last 24 hours with the subject "Urgent Action Required on Your Account."
3.  **Review the Results:** Explorer returns a list of every user who received that email. The analyst can review the emails to confirm they are all part of the same malicious campaign and are not legitimate communications.
4.  **Remediate (The "Zap"):** Once confirmed, the analyst selects all the malicious emails in the results and chooses an action. The most common action is a **"Soft delete,"** which moves the emails to the users' Recoverable Items folder (like a second-stage recycle bin). This removes the immediate threat from the inbox but allows for recovery if a mistake was made.
5.  **Investigate Further:** After removing the threat, the analyst would investigate who might have clicked the malicious link or opened the attachment to determine if any accounts were compromised or if any computers were infected.
