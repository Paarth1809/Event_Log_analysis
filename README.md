# Windows Event Log Analysis After RDP Brute Force Attack

## Overview
This lab demonstrates how to detect and investigate an **RDP brute-force attack** using **Windows Event Viewer** after simulating the attack with **Hydra** from a Kali Linux machine.

## Lab Environment

| Machine | IP Address | Role |
|---------|------------|------|
| Kali Linux | `192.168.9.129` | Attacker |
| Windows 10 | `192.168.9.128` | Victim |

---

## Objective

- Simulate an RDP brute-force attack.
- Generate Windows Security logs.
- Analyze authentication events using Event Viewer.
- Identify brute-force indicators.
- Filter and export logs for investigation.

---

## Tools Used

- Kali Linux
- Windows 10
- Hydra
- Windows Event Viewer

---

## RDP Configuration

Remote Desktop (RDP) was enabled on the Windows machine to allow remote authentication.

> **Figure 1:** Enable RDP on Windows

---

## Windows Event Viewer

Windows Event Viewer continuously records system, application, and security events.

Common Event IDs used during authentication:

| Event ID | Description |
|----------|-------------|
| **4624** | Successful Logon |
| **4625** | Failed Logon |

> **Figure 2:** Event Viewer

---

## Brute Force Attack

Hydra was used to perform an RDP brute-force attack against the Windows machine.

```bash
hydra -t 4 -V -f -l administrator -P rockyou.txt rdp://192.168.9.128
```

### Command Breakdown

- `-t 4` → 4 parallel tasks
- `-V` → Verbose output
- `-f` → Stop after first successful password
- `-l administrator` → Username
- `-P rockyou.txt` → Password wordlist

> **Figure 3:** Windows IP

> **Figure 4:** Kali IP

> **Figure 5:** Hydra Attack

---

## Log Analysis

After the attack, Windows Event Viewer showed a large number of failed login attempts within a very short period.

Indicators observed:

- Multiple Event ID **4625** entries
- Repeated authentication failures
- High login frequency
- Signs of a brute-force attack

> **Figure 6:** Log Analysis

---

## Filtering Security Logs

Instead of reviewing every log manually, Event Viewer allows filtering by:

- Event ID
- Keywords
- User
- Event Level
- Task Category
- Log Source

Filtering helps SOC analysts quickly identify suspicious events.

> **Figure 7:** Log Filtering

---

## Event Details

Opening an individual event provides valuable forensic information, including:

- Event ID
- Timestamp
- Source IP Address
- Source Port
- Workstation Name
- Logon Type
- Username

> **Figure 8:** Detailed Event Properties

---

## Exporting Logs

Security logs can be exported for:

- Incident response
- Sharing with senior analysts
- Further forensic investigation
- Evidence preservation

Windows also supports remote viewing of Event Logs without exporting them.

> **Figure 9:** Exporting Logs

---

## Detection Summary

| Indicator | Observation |
|-----------|-------------|
| Attack Type | RDP Brute Force |
| Detection Method | Windows Event Viewer |
| Primary Event ID | 4625 |
| Log Source | Windows Security Logs |
| Analysis Method | Event Filtering & Event Properties |

---

## Skills Demonstrated

- Windows Log Analysis
- Event Viewer Investigation
- Authentication Monitoring
- RDP Attack Detection
- Hydra Simulation
- Security Event Filtering
- Basic Incident Investigation

---

## Conclusion

This lab simulated an RDP brute-force attack using Hydra and demonstrated how Windows Event Viewer can be used to detect authentication attacks through Event ID analysis. By filtering security events and examining detailed log information, it was possible to identify brute-force activity and collect evidence for further investigation.

---

## Author

**Parth Srivastava**

Cybersecurity | SOC Analyst | Blue Team
