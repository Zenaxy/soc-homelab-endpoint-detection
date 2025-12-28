# Detection Analysis – Endpoint Malware Activity

## 🕒 Timeline Summary

This section summarizes the observed activity during the lab simulation:

1. Attacker machine performed network reconnaissance against the Windows endpoint
2. A suspicious executable was downloaded and executed on the endpoint
3. The endpoint established an outbound network connection to the attacker machine
4. The attacker executed basic system commands through the established session

These actions generated endpoint telemetry captured by Sysmon and analyzed in Splunk.

---

## 🔎 Detection 1 – Suspicious Process Creation  
**(Sysmon Event ID 1)**

### Observation
A non-standard executable was executed on the Windows system and spawned a command-line interpreter.

### Key Fields Observed
- `Image`
- `ParentImage`
- `CommandLine`
- `User`

### Analysis
The parent process was an unusual executable file that spawned `cmd.exe` as a child process.  
This parent-child relationship is abnormal for standard user activity and is commonly observed in malware execution scenarios.

Such behavior often indicates:
- Initial malware execution
- Payload execution
- Post-exploitation command handling

---

## 🌐 Detection 2 – Suspicious Network Connection  
**(Sysmon Event ID 3)**

### Observation
The Windows endpoint initiated an outbound network connection to another host within the lab network.

### Key Fields Observed
- `SourceIp`
- `DestinationIp`
- `DestinationPort`
- `Image`

### Analysis
The connection was established shortly after the suspicious process execution and originated from the same executable.  
The destination port used is commonly associated with reverse shell activity in lab and testing scenarios.

This pattern suggests command-and-control–style behavior, where the compromised endpoint initiates communication outward.

---

## 🧬 Detection 3 – Process Tree Analysis

### Observation
The suspicious executable spawned multiple child processes during execution.

### Analysis
Process tree analysis revealed the following behavior:
- Initial executable launched
- Child command-line process spawned
- System commands executed via the child process

This behavior is consistent with post-exploitation activity such as:
- Host enumeration
- Privilege context discovery
- Environment reconnaissance

Process tree visibility proved critical in understanding the full scope of activity.

---

## 🧠 Conclusion

This lab demonstrates how simulated attacker behavior generates clear and detectable endpoint telemetry.

Even without knowing the payload contents, defenders can identify malicious activity by analyzing:
- Process creation patterns
- Parent-child process relationships
- Network connection behavior

Sysmon combined with Splunk provides strong visibility into endpoint activity and supports effective detection of suspicious behavior.

---

## 📘 Lessons Learned

- Endpoint telemetry is essential for SOC visibility
- Process relationship analysis is a powerful detection technique
- Correlating process and network events increases detection confidence
- SIEM platforms enable defenders to identify threats early in the attack lifecycle
