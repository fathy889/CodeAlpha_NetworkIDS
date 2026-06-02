# 🛡️ CodeAlpha Network Intrusion Detection System
## Task 4 | Cyber Security Internship

**Tool:** Suricata 8.0.5
**Reviewer:** [fathy wael]
**Platform:** Kali Linux

---

## Description

A Network Intrusion Detection System (NIDS) built using Suricata.
Monitors live network traffic and detects suspicious or malicious activity
using both Emerging Threats rules and custom detection rules.

---

## What Was Detected

| Alert | Rule | Severity |
|-------|------|----------|
| GPL ATTACK_RESPONSE id check returned root | ET Open Rules | High |
| Nmap Port Scan Detected | Custom Rule sid:9000003 | Medium |

---

## Custom Rules

### Rule 1: ICMP Ping Scan
alert icmp any any -> $HOME_NET any (msg:"ICMP Ping Scan Detected"; itype:8; threshold:type threshold, track by_src, count 5, seconds 2; sid:9000001; rev:1;)

### Rule 2: SSH Brute Force
alert tcp any any -> $HOME_NET 22 (msg:"SSH Brute Force Attempt"; flow:to_server,established; threshold:type threshold, track by_src, count 5, seconds 10; sid:9000002; rev:1;)

### Rule 3: Nmap Port Scan
alert tcp any any -> $HOME_NET any (msg:"Nmap Port Scan Detected"; flags:S; threshold:type threshold, track by_src, count 20, seconds 3; sid:9000003; rev:1;)

### Rule 4: SQL Injection Attempt
alert http any any -> any any (msg:"SQL Injection Attempt Detected"; content:"union select"; nocase; http_uri; sid:9000004; rev:1;)

### Rule 5: Command Injection Attempt
alert http any any -> any any (msg:"Command Injection Attempt Detected"; content:"/etc/passwd"; http_uri; sid:9000005; rev:1;)

---

## How to Run

Install Suricata:
sudo apt install suricata -y

Update rules:
sudo suricata-update

Copy custom rules:
sudo cp local.rules /etc/suricata/rules/local.rules

Run Suricata:
sudo suricata -i eth0 -l /tmp/suricata-logs/

View alerts:
cat /tmp/suricata-logs/fast.log

---

## Sample Output

06/02/2026-14:31:21 [**] GPL ATTACK_RESPONSE id check returned root [**] [Priority: 2] {TCP} 3.175.86.5:80 -> 10.0.2.15:49170
06/02/2026-14:54:55 [**] Nmap Port Scan Detected [**] [Priority: 3] {TCP} 10.0.2.15:40610 -> 10.0.2.2:113

---

## Project Structure

CodeAlpha_NetworkIDS/
├── local.rules       # Custom Suricata detection rules
├── fast.log          # Sample alerts captured during testing
└── README.md         # Project documentation

---

*CodeAlpha Cyber Security Internship — Task 4*
