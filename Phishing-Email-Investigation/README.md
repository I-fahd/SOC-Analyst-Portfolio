
# 🚨 Incident Report: SOC141 - Phishing URL Detected

**Case ID:** 86  
**Platform:** LetsDefend  
**Date:** 2026-1-12  
**Verdict:** True Positive 

---

## 📝 1. Executive Summary  

**Description:** An internal host (**EmilyComp**) attempted to access a known malicious URL hosted on a Russian domain (`mogagrocol.ru`). The host was successfully contained, and the destination IP was blocked at the firewall level.
---

## 🔍 2. Analysis & Investigation

### 2.1 Trigger Event
The SIEM triggered an alert for "Phishing URL Detected" Based on threat intelligence feeds.
* **Alert Time:** Mar, 22, 2021, 09:23 PM
* **Source IP / Host:** 172.16.17.49 / EmilyComp
* **Suspicious URL:** http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io

### 2.2 Investigation Steps

#### Step 1: Verification of Activity
I analyzed the **Log Management** tab to verify if the user actully connected to the site.
* **Observation:** the logs showed **2 successful http connections** at proxy and firewall layer, meaning the user visited the malicious site.
* **Evidence:**
    > ![Log Activity Screenshot](https://github.com/I-fahd/Cybersecurity_labs/blob/3a98a2a5cb29184cfd110cbc05ca633226027981/Phishing-Email-Investigation/logs.png)

#### Step 2: Threat Intelligence Check
I checked the URL address in VirusTotal.
* **VirusTotal Result:** 12/97 security vendors flagged this URL as malicious
* **Evidence:**
    > ![VirusTotal Screenshot](virustotal.png)

#### Step 3: Endpoint Analysis
I checked endpoint security for EmilyComp to see if any files were downloaded.
Downloads: No files were downloaded

---

## 🛡️ 3. Containment & Remediation
Based on the analysis, the alert was deemed a **True Positive**. The following actions were taken:

1.  **Isolation:** The machine `EmilyComp` was isolated from the network to via EDR to prevent potential C2 communication..
2.  **Blocking:** The IP 91.189.114.8 was added to the Firewall Blocklist.
---

## 🔬 4. Indicators of Compromise (IOCs)
The following artifacts were collected during the investigation:

| Type | Value | Description |
| :--- | :--- | :--- |
| **IP Address** | `91.189.114.8` | Hosting Server (Russia) |
| **Domain** | `mogagrocol.ru` | Phishing Domain |
| **URL Pattern** | `.../index.php?email=` | Credential Harvesting Pattern |

---

## 🧠 5. Analyst Notes & Lessons Learned
* Lesson Learned: The firewall allowed this connection because the domain was newly registered and had not yet propagated to our threat feeds. I recommended tuning the firewall to block uncategorized domains.

