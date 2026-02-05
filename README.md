# Real-Time File Integrity Monitoring (FIM) with Wazuh

**Author:** Muhammad Zubair (@mrsonic9)  
**Domain:** Defensive Security / Blue Teaming  
**Tools:** Wazuh SIEM, Windows 10 Endpoint, Syscheck

## 📌 Project Overview
In this project, I configured the Wazuh SIEM to perform real-time File Integrity Monitoring (FIM) on a Windows endpoint. The goal was to detect unauthorized modifications, creations, or deletions of files in sensitive user directories—a critical control for detecting ransomware and insider threats.

## ⚙️ Network Architecture
* **Wazuh Manager:** Hosted on Linux (Ubuntu).
* **Wazuh Agent:** Installed on Windows 10 (Target Machine).
* **Connection:** Agent authenticated and communicating via port 1514.

## 🚀 Implementation Steps

### 1. Configuring the Windows Agent
I modified the Wazuh agent configuration file (`ossec.conf`) on the Windows endpoint to target specific user directories. I enabled `realtime="yes"` to ensure alerts are triggered instantly rather than waiting for scheduled scans.

**Code Configuration:**
```xml
<directories check_all="yes" realtime="yes">C:\Users\zubair\Documents</directories>

<br>

---

## 🛡️ Part 2: Active Response (Automated Defense)

Moving beyond detection, I configured an **Intrusion Prevention System (IPS)** capability to automatically block attackers attempting to brute-force access to the Windows endpoint.

### 1. The "Brain" (Manager Configuration)
I configured the Wazuh Manager to trigger a defensive script whenever it detects a **Brute Force Attack** (Rule ID 60122 - Multiple Failed Logins).

**Configuration (`ossec.conf`):**
```xml
<command>
  <name>win_route-null</name>
  <executable>route-null.exe</executable>
  <expect>srcip</expect>
  <timeout_allowed>yes</timeout_allowed>
</command>

<active-response>
  <command>win_route-null</command>
  <location>local</location>
  <rules_id>60122</rules_id>
  <timeout>60</timeout>
</active-response>
