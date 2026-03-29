# 🔐 SSH Brute Force Detection Lab

## 📌 Project Overview

This project simulates an SSH brute-force attack on a Linux system and demonstrates how authentication logs can be analyzed to detect suspicious login activity.

The goal was to simulate attacker behavior, generate failed login attempts, and investigate authentication logs like a SOC (Security Operations Center) analyst.

---

## 🛠️ Lab Environment

| Component | Details |
|-----------|---------|
| Operating System | Ubuntu Linux |
| Service Used | OpenSSH Server |
| Log Source | `/var/log/auth.log` |
| Attack Simulation | Failed SSH login attempts |

---

## ⚙️ System Configuration

SSH service was installed and enabled using the following commands:
```bash
sudo apt install openssh-server -y
sudo systemctl start ssh
sudo systemctl enable ssh
sudo systemctl status ssh
```

Firewall configuration:
```bash
sudo ufw allow ssh
sudo ufw enable
sudo ufw status
```

---

## 👤 Attacker Simulation

A test user was created to simulate attacker login attempts:
```bash
sudo adduser attackeruser
```

SSH login attempts were performed using incorrect passwords:
```bash
ssh attackeruser@192.168.0.168
```

Multiple incorrect passwords were entered to generate failed authentication logs.

---

## 🔎 Log Investigation

Failed login attempts were identified using:
```bash
grep "Failed password" /var/log/auth.log
```

Total failed login attempts:
```bash
grep "Failed password" /var/log/auth.log | wc -l
```

First failed login:
```bash
grep "Failed password" /var/log/auth.log | head -n 1
```

Last failed login:
```bash
grep "Failed password" /var/log/auth.log | tail -n 1
```

---

## 📊 Attack Timeline

| Field | Details |
|-------|---------|
| Attack Type | SSH Brute Force |
| Target Username | attackeruser |
| Source IP Address | 192.168.0.168 |
| Total Failed Attempts | 5 |
| First Failed Login | *(Paste your head -n 1 output here)* |
| Last Failed Login | *(Paste your tail -n 1 output here)* |

---

## ⚠️ Risk Impact

Repeated failed SSH login attempts indicate a brute-force attack attempt. If successful, attackers could gain unauthorized access to the system, leading to data compromise, privilege escalation, or system misuse.

---

## 🛡️ Recommended Actions

- Enforce strong password policies
- Implement account lockout after multiple failed login attempts
- Restrict SSH access to trusted IP addresses
- Enable Fail2Ban to block repeated attackers
- Monitor authentication logs regularly

---

## 📸 Screenshots

The following screenshots were captured during the investigation:

1. SSH service status
2. Attacker user creation
3. Failed SSH login attempts
4. Authentication log analysis
5. Attack timeline extraction

---

## 🎯 Skills Demonstrated

- Linux System Administration
- SSH Configuration
- Log Analysis
- Incident Investigation
- Threat Detection
- Cybersecurity Fundamentals

---

## 🔗 Connect

**Author:** Alex Ojo
Cybersecurity Student | SOC Analyst Trainee

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/alex-o-ojo-ab9252185)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black)](https://github.com/alexojocyber)
