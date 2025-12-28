# soc-homelab-endpoint-detection
# Endpoint Attack Detection using Sysmon &amp; Splunk (SOC Home Lab)  This project demonstrates how endpoint attack activities generate telemetry and how those events can be detected and analyzed using Sysmon and Splunk in a SOC-style home lab environment.


## 📌 Project Overview

This project focuses on **detecting malicious endpoint activity** rather than exploiting systems.

Using a controlled home lab, I simulated common attack behaviors such as network scanning and reverse TCP malware execution to observe the telemetry generated on a Windows endpoint and analyze it using Splunk.

The main goal is to understand:
- What logs are generated during an attack
- How to analyze those logs in Splunk
- How to build simple detection logic from endpoint telemetry

