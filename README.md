# Fine-Tuned Sysmon Configuration for Wazuh

This repository contains a **fine-tuned Sysmon configuration file** designed to enhance security monitoring and log collection for **Wazuh SIEM**. The configuration is optimized to **reduce noise, capture high-value security events**, and improve threat detection efficiency.

## 🔹 Features & Improvements
- **Focused Event Logging**: Includes essential Sysmon events while filtering out unnecessary noise.
- **Enhanced Detection**: Captures critical security events such as process creation, network connections, registry changes, and DNS queries (**Event ID 22**).
- **Optimized for Wazuh**: Ensures compatibility with Wazuh’s **Sysmon rule set** for better alerting and correlation.
- **Performance Considerations**: Minimizes excessive logging to prevent storage and processing overhead.

## 📌 Key Logged Events
- **Process Execution (Event ID 1)**
- **File Creation (Event ID 11)**
- **Registry Modifications (Event ID 13-14)**
- **DNS Queries (Event ID 22)**
- **Network Connections (Event ID 3)**
- **Named Pipe Events (Event ID 17-19)**
- **WMI Activity (Event ID 19-20)**

## 📖 Installation & Usage
1. **Download** the `sysmon.xml` file from this repository.
2. **Deploy** it on your Windows system with Sysmon:
   ```powershell
   sysmon -c sysmon.xml
   ```
3. Ensure Wazuh is configured to collect **Sysmon logs** from:
   ```
   Microsoft-Windows-Sysmon/Operational
   ```
4. **Restart Sysmon** to apply the new configuration:
   ```powershell
   net stop sysmon && net start sysmon
   ```

## 💡 Notes
- This configuration is **customizable**. You can modify or extend the event filtering rules based on your security needs.
- If using with Wazuh, ensure the **Sysmon rules are enabled** in `sysmon_rules.xml`.
- Logs are stored in **Windows Event Viewer** under:
  ```
  Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
  ```

## 📜 License
This project is licensed under the **MIT License** – feel free to use and modify it as needed!

## 🤝 Contributions
Contributions are welcome! Feel free to submit **pull requests** or open an **issue** if you have suggestions or improvements.

## 📧 Contact
For any questions or discussions, reach out via GitHub issues.

---
🚀 **Stay secure & happy monitoring!**
