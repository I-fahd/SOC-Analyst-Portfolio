# 🚨 Incident Report: SOC114 - Malicious Attachment Detected

**Case ID:** 45
**Platform:** LetsDefend
**Date:** 2021-01-31
**Verdict:** True Positive

---

## 📝 1. Executive Summary
**Alert Severity:** High
**Status:** Closed

**Description:**
A phishing email containing a malicious Excel attachment (`Invoice.xlsx`) was delivered to an internal user (**Richard**). The attachment utilized a known Microsoft Office vulnerability (CVE-2017-11882) to execute malicious code. The host was successfully compromised as the user opened the file, triggering a credential dumping tool (`LaZagne.exe`). The device was isolated, and the malicious email was deleted.

---

## 🔍 2. Analysis & Investigation

### 2.1 Trigger Event
The SIEM triggered an alert for a "Malicious Attachment" based on mail gateway filters.
* **Alert Time:** Jan 31, 2021, 15:48
* **Sender:** `accounting@cmail.carleton.ca`
* **Recipient:** `richard@letsdefend.io`
* **Subject:** Invoice
* **Attachment:** `Invoice.xlsx`

### 2.2 Investigation Steps

#### Step 1: Email Analysis
I analyzed the **Log Management** tab to verify if the email was delivered.
* **Result:** The "Device Action" was **Allowed**, meaning the email reached the user's inbox.
* **Evidence:**
    > ![Email Log Screenshot](email_log.png)

#### Step 2: Attachment Analysis (Static)
I downloaded the attachment `Invoice.xlsx` and analyzed its hash in VirusTotal.
* **SHA256:** `44e65a641fb970031c5efed324676b5018803e0a768608d3e186152102615795`
* **VirusTotal Result:** **Malicious** (Flagged by multiple vendors).
* **Exploit Detected:** CVE-2017-11882 (Microsoft Equation Editor RCE).
* **Evidence:**
    > ![VirusTotal Screenshot](virustotal.png)

#### Step 3: Endpoint Analysis (Dynamic)
I checked **Endpoint Security** for the host `Richard` to see if the file was executed.
* **Process:** `LaZagne.exe`.
* **Observation:** The presence of `LaZagne.exe` (a known credential harvesting tool) confirms that the exploit was successful and the machine is compromised.
* **Evidence:**
    > ![Process Screenshot](process.png)

---

## 🛡️ 3. Containment & Remediation
Based on the analysis, the alert was deemed a **True Positive**.

**Immediate Actions:**
1.  **Isolation:** The host `Richard` was isolated from the network to prevent data exfiltration.
2.  **Email Purge:** The malicious email was deleted from the user's mailbox.
   
---

## 🔬 4. Indicators of Compromise (IOCs)

| Type | Value | Description |
| :--- | :--- | :--- |
| **Sender Email** | `accounting@cmail.carleton.ca` | Phishing Sender |
| **File Hash (SHA256)** | `44e65a641...795` | Malicious Excel File |
| **Malware** | `LaZagne.exe` | Credential Dumping Tool |

---

## 🧠 5. Analyst Notes
* **Root Cause:** The user opened an attachment from an external, unverified sender.
* **Recommendation:** Patch Microsoft Office to the latest version to mitigate CVE-2017-11882. Conduct phishing awareness training for the user (Richard).
