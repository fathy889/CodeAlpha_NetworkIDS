# 🛡️ Network Intrusion Detection System
### Task 4 | Cyber Security Internship
---
## 📌 Description
A **Network Intrusion Detection System (NIDS)** built using **Suricata 8.0.5**. Monitors live network traffic in real time and detects suspicious or malicious activity using **50,402 Emerging Threats rules** + **5 custom detection rules**.
---
## 🚨 Attacks Detected
| Alert | Source | Severity |
|-------|--------|----------|
| GPL ATTACK_RESPONSE id check returned root | ET Open Rules | 🔴 High |
| Nmap Port Scan Detected | Custom Rule sid:9000003 | 🟡 Medium |
---
## 📋 Custom Rules
| SID | Rule | Detects |
|-----|------|---------|
| 9000001 | ICMP Ping Scan | Ping flood / host discovery |
| 9000002 | SSH Brute Force | Repeated SSH login attempts |
| 9000003 | Nmap Port Scan | SYN scan / port enumeration |
| 9000004 | SQL Injection | union select in HTTP URI |
| 9000005 | Command Injection | /etc/passwd in HTTP URI |
---
## 🚀 How to Run
```bash
# 1. Install Suricata
sudo apt install suricata -y
# 2. Update rules
sudo suricata-update
# 3. Copy custom rules
sudo cp local.rules /etc/suricata/rules/local.rules
# 4. Run Suricata
sudo suricata -i eth0 -l /tmp/suricata-logs/
# 5. View alerts
cat /tmp/suricata-logs/fast.log
# 6. Live monitoring
tail -f /tmp/suricata-logs/fast.log
```
---
## 📡 Sample Output
```
06/02/2026-14:31:21  [**] GPL ATTACK_RESPONSE id check returned root [**] [Priority: 2] {TCP} 3.175.86.5:80 -> 10.0.2.15:49170
06/02/2026-14:54:55  [**] Nmap Port Scan Detected [**] [Priority: 3] {TCP} 10.0.2.15:40610 -> 10.0.2.2:113
```
---
## 📁 Project Structure
```
CodeAlpha_NetworkIDS/
├── local.rules    # 5 custom Suricata detection rules
├── fast.log       # Sample alerts captured during testing
└── README.md      # Project documentation
```
---
## 👤 Author
**Fathy Wael** — Cyber Security Intern
GitHub: [@fathy889](https://github.com/fathy889)
---
*Cyber Security Internship — Task 4*
