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
