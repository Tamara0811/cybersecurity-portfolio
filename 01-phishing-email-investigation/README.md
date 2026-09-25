# Phishing Email Investigation

## Project Overview

This project documents a simulated phishing email investigation from the perspective of a Tier 1 SOC analyst.
## Scenario

A suspicious email impersonating Microsoft Windows was delivered to a user's inbox and allowed by the email security system. The email advertised a free Windows 11 Pro upgrade and instructed the recipient to perform unusual actions on their Windows device.

## Objective

The objective of this investigation was to determine whether the email was benign or malicious by analyzing the sender information, email content, social engineering indicators, and available indicators of compromise (IOCs).

## Tools Used

- LetsDefend
- VirusTotal
## Investigation & Findings

### 1. Sender Analysis

- Sender: `update@windows-update.site`
- Sender IP: `132.232.40.201`
- Recipient: `dylan@letsdefend.io`
- Subject: `Upgrade your system to Windows 11 Pro for FREE`
- Email Security Action: `Allowed`
### Initial Observations

- The sender domain appeared suspicious and attempted to impersonate Microsoft/Windows.
- Several images in the email were broken or failed to load.
- The email used a countdown timer to create a sense of urgency and encourage the recipient to act quickly.
- The email provided unusual instructions asking the recipient to open the Windows Run dialog, paste clipboard content, and execute it.

 ### 2. IOC Reputation Analysis

The sender IP address and domain were investigated using VirusTotal to gather additional threat intelligence.

**Sender IP:** `132.232.40.201`
- 2/91 security vendors flagged the IP address as malicious.
- The result was treated as a supporting indicator rather than definitive proof of malicious activity.

**Sender Domain:** `windows-update.site`
- 11/91 security vendors flagged the domain as malicious.
- The domain reputation provided stronger supporting evidence that the email may be associated with malicious activity.

### 3. Analysis

The VirusTotal results were not used as the only reason to classify the email as malicious. They provided additional evidence that supported the suspicious indicators already identified in the email. The domain reputation was particularly significant, with 11/91 security vendors flagging `windows-update.site` as malicious. Combined with the domain impersonation, urgency tactics, and instructions to execute pasted content through the Windows Run dialog, the evidence strongly indicated malicious activity.

## Final Verdict

**Classification:** Malicious

The email was classified as malicious based on the combination of Microsoft/Windows impersonation, social engineering techniques, suspicious execution instructions, and negative threat-intelligence results associated with the sender infrastructure.

The available evidence confirms that the email presented a security risk. However, the available telemetry does not show whether the recipient followed the instructions or whether the endpoint was compromised.

## Recommended Response

- Quarantine and remove the malicious email from the recipient's mailbox.
- Search for and remove the same email from other users' mailboxes.
- Block the malicious sender domain and review the sender IP for appropriate blocking.
- Contact the recipient to determine whether they followed the instructions in the email.
- If the recipient executed the instructions, escalate the incident for endpoint investigation and potential containment.

## MITRE ATT&CK Mapping

**T1566 – Phishing:** The attack used a deceptive email impersonating Microsoft/Windows to influence the recipient into performing potentially unsafe actions.

Additional execution techniques were not mapped because the available evidence did not reveal the command or payload and did not confirm that the recipient executed the instructions.

## Lessons Learned

- Learned how to use VirusTotal to investigate the reputation of domains and IP addresses during an email investigation.
- Learned how phishing activity can be mapped to the MITRE ATT&CK framework using technique identifiers such as T1566 (Phishing).
- Learned that threat-intelligence results should be correlated with other evidence rather than used alone to determine whether an email is malicious.
