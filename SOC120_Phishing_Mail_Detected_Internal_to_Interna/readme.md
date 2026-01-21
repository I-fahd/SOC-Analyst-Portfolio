# 🚨 Incident Report: SOC120 - Phishing Mail Detected - Internal to Internal

**Case ID:** 52
**Platform:** LetsDefend
**Date:** 2026-1-22
**Verdict:** False Positive

---

## 📝 1. Executive Summary
**Alert Severity:** Medium
**Status:** Closed

**Description:**
A phishing alert was triggered for an email sent between two internal employees (**John** to **Susie**). Investigation revealed that the email has not any attachment or url. So the phishing alert was false positive.

---

## 🔍 2. Analysis & Investigation

### 2.1 Trigger Event
The SIEM triggered an alert for "Phishing Mail Detected - Internal to Internal."
* **Alert Time:**  Feb, 07, 2021, 04:24 AM
* **Sender:** `john@letsdefend.io` (Internal)
* **Recipient:** `susie@letsdefend.io` (Internal)
* **Subject:** `Meeting`
* **Attachment:** `No attachment or url included`

### 2.2 Investigation Steps

#### Step 1: Header & Log Analysis
I analyzed the **Log Management** tab to verify the source.
* **Source IP:** The email originated from a local internal IP, confirming it was NOT a spoofed external email, but genuinely sent from John's account.
* **Conclusion:** **Normal behavior**.

#### Step 2: Attachment Analysis
I cheched **Email Security** to see if the eamil content is suspicicous and if there is any attachment or url.
* **Conclusion:** The content is noraml and there is no any attachment or url.
* **Evidence:**
    > ![Email Screenshot](email_security.png)

---

## 🛡️ 3. Containment & Remediation
Based on the analysis, the alert was deemed a **False Positive**.

**There was not Actions Taken**

---

## 🔬 4. Indicators of Compromise (IOCs)

| Type | Value | Description |
| :--- | :--- | :--- |

---

## 🧠 5. Analyst Notes
* **Recommendation:** Tuning the SEIM to decrese false positive alerts.
