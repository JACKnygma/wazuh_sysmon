# wazuh_sysmon
This repository contains a fine-tuned Sysmon configuration file designed to enhance security monitoring and log collection for Wazuh SIEM. The configuration is optimized to reduce noise, capture high-value security events, and improve threat detection efficiency.
🔹 Features & Improvements
Focused Event Logging: Includes essential Sysmon events while filtering out unnecessary noise.
Enhanced Detection: Captures critical security events such as process creation, network connections, registry changes, and DNS queries (Event ID 22).
Optimized for Wazuh: Ensures compatibility with Wazuh’s Sysmon rule set for better alerting and correlation.
Performance Considerations: Minimizes excessive logging to prevent storage and processing overhead.
📌 Key Logged Events
Process Execution (Event ID 1)
File Creation (Event ID 11)
Registry Modifications (Event ID 13-14)
DNS Queries (Event ID 22)
Network Connections (Event ID 3)
Named Pipe Events (Event ID 17-19)
WMI Activity (Event ID 19-20)

