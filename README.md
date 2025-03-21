# Integrating Wazuh with Sysmon for Enhanced Security Monitoring

This guide provides step-by-step instructions for integrating **Sysmon** with **Wazuh** to improve Windows event monitoring and threat detection. It leverages the **SwiftOnSecurity Sysmon configuration** and a custom **Wazuh rule set** to efficiently capture and analyze security-relevant events.

## 📌 Prerequisites
- **Wazuh Server** is already installed and running.
- **Wazuh Agent** is installed on the Windows endpoint.
- **Administrator access** on the Windows machine.

## 🛠 Step 1: Install Sysmon with Recommended Configuration
We will use the well-maintained **Sysmon configuration** from [SwiftOnSecurity](https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml) to ensure high-quality event filtering.

1. **Download Sysmon & Configuration**:
   ```powershell
   Invoke-WebRequest -Uri https://download.sysinternals.com/files/Sysmon.zip -OutFile Sysmon.zip
   Expand-Archive -Path Sysmon.zip -DestinationPath .
   Invoke-WebRequest -Uri https://raw.githubusercontent.com/SwiftOnSecurity/sysmon-config/master/sysmonconfig-export.xml -OutFile sysmonconfig.xml
   ```
2. **Install Sysmon with the Configuration**:
   ```powershell
   sysmon -accepteula -i sysmonconfig.xml
   ```
3. **Verify Sysmon Installation**:
   ```powershell
   sysmon -c
   ```
   - Ensure Sysmon is running and collecting logs.
   - Logs will appear in **Event Viewer** under:
     ```
     Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
     ```

## ⚙️ Step 2: Configure Wazuh Agent to Collect Sysmon Logs
Now, we will configure the Wazuh agent to read **Sysmon logs** and apply the custom rules from this repository.

1. **Edit the Wazuh Agent Configuration File**:
   - Open the Wazuh agent config file (`ossec.conf`) located at:
     ```
     C:\Program Files (x86)\ossec-agent\ossec.conf
     ```
   - Add the following section inside `<localfile>` tags:
     ```xml
     <localfile>
       <log_format>eventchannel</log_format>
       <location>Microsoft-Windows-Sysmon/Operational</location>
     </localfile>
     ```

2. **Add Fine-Tuned Wazuh-Sysmon Rules for Sysmon**:
   - The wazuh has default rules for Sysmon. But for more data enrichments and visibility, 
     you can use the **.xml** file from **wazuh_sysmon-rule folder**
   
3. **Restart Wazuh Services**:
   - Restart the Wazuh agent on Windows:
     ```powershell
     net stop wazuh-agent && net start wazuh-agent
     ```
   - Restart the Wazuh manager to apply new rules:
     ```bash
     sudo systemctl restart wazuh-manager
     ```

## 🛠 Step 3: Verify Integration
1. Generate test events by opening **Event Viewer** and checking **Sysmon logs**.
2. Check the Wazuh **alerts.log** file to ensure Sysmon events are processed:
   ```bash
   tail -f /var/ossec/logs/alerts/alerts.json | jq '.'
   ```
3. View alerts in **Wazuh Dashboard** under **Security Events**.

## 📜 Credits
- **Sysmon Configuration**: [SwiftOnSecurity](https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml)
- **Wazuh Rules & Integration Guide**: This repository

---
🚀 **Now, your Wazuh and Sysmon setup is ready for advanced threat detection!**
