# Detection Analysis – Malware Execution

## 🕒 Timeline Summary
1. Attacker performed reconnaissance activity
2. Malicious executable was executed on Windows endpoint
3. Reverse TCP connection established
4. Attacker executed system commands

---

## 🔎 Detection 1 – Process Creation (Sysmon Event ID 1)

**Observation:**
A suspicious executable was launched on the system.

**Key Fields:**
- Image
- ParentImage
- CommandLine
- User

**Analysis:**
The process shows an unusual parent-child relationship where a non-standard executable spawns `cmd.exe`.  
This behavior is commonly associated with malware execution.

---

## 🌐 Detection 2 – Network Connection (Sysmon Event ID 3)

**Observation:**
An outbound network connection was detected.

**Key Fields:**
- Source IP
- Destination IP
- Destination Port
- Image

**Analysis:**
The endpoint initiated a connection to an external IP on a high-risk port, consistent with reverse shell behavior.

---

## 🧬 Detection 3 – Process Tree Analysis

**Observation:**
The malicious executable spawned multiple child processes.

**Analysis:**
Malware often spawns system utilities to perform post-exploitation activities such as enumeration and persistence.

---

## 🧠 Conclusion
This lab demonstrates how basic attacker behavior generates detectable telemetry.  
By analyzing Sysmon logs in Splunk, defenders can identify suspicious activity even without knowing the payload details.

---

## 📘 Lessons Learned
- Endpoint telemetry is critical for detection
- Parent-child process analysis is highly effective
- SIEM visibility enables early detection of compromise
