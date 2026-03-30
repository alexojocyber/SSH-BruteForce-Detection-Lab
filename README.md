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
| First Failed Login | Mar 29 13:44:45 — Failed password for attackeruser from 192.168.0.168 |
| Last Failed Login | Mar 29 13:46:35 — Failed password for attackeruser from 192.168.0.168 |

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
<img width="1306" height="988" alt="ssh-service-running" src="https://github.com/user-attachments/assets/f7ebc51f-7345-4d7b-9290-985fe888d328" />


2. Attacker user creation
<img width="862" height="136" alt="attacker-user-created" src="https://github.com/user-attachments/assets/cfacbe3b-a086-4cef-900d-d0ca1cd947e4" />


3. Failed SSH login attempts
<img width="1845" height="999" alt="failed-ssh-login-attempt" src="https://github.com/user-attachments/assets/3e50bc69-938b-4703-a472-99924092247a" />


4. Authentication log analysis
<img width="1859" height="490" alt="failed-password-logs" src="https://github.com/user-attachments/assets/e6a6ce4d-03db-4940-8bc3-33a80a960db8" />

5. Attack timeline extraction
<img width="908" height="51" alt="failed-attempt-count" src="https://github.com/user-attachments/assets/b75ee034-37d9-460a-b0ec-5dfacbb32759" />

<img width="1550" height="57" alt="first-attack" src="https://github.com/user-attachments/assets/49d96fc8-f24e-41a9-8e00-843ee802eeb8" />

<img width="1842" height="140" alt="last-attack" src="https://github.com/user-attachments/assets/66dc3571-0d27-458e-961c-9042f8738f5b" />

---

## 🎯 Skills Demonstrated

- Linux System Administration
- SSH Configuration
- Log Analysis
- Incident Investigation
- Threat Detection
- Cybersecurity Fundamentals

---

## 🛡️ Defense Implementation — Fail2Ban

After detecting repeated failed SSH login attempts, Fail2Ban was installed to automatically block attackers after multiple failed login attempts.

### 📦 Installing Fail2Ban
```bash
sudo apt update
sudo apt install fail2ban -y
```

Fail2Ban service was started and enabled:
```bash
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
sudo systemctl status fail2ban
```

---

### ⚙️ SSH Protection Configuration

A Fail2Ban rule was created to monitor SSH login failures.

Configuration file:
```bash
sudo nano /etc/fail2ban/jail.local
```

Configuration used:
```ini
[sshd]
enabled = true
port = ssh
maxretry = 3
bantime = 600
findtime = 300
```

This configuration blocks an IP address after **3 failed login attempts** within **5 minutes**, banning the attacker for **10 minutes**.

---

### 🚫 Attack Prevention Test

Multiple failed SSH login attempts were generated again to trigger Fail2Ban protection.

Fail2Ban status was checked using:
```bash
sudo fail2ban-client status sshd
```

Result:
```
Currently banned: 1
```

This confirms that the attacker IP was successfully blocked.

---

### 📸 Fail2Ban Screenshots

The following screenshots demonstrate the defense implementation:

- Fail2Ban service running
<img width="1847" height="997" alt="fail2ban-running" src="https://github.com/user-attachments/assets/5a0c0fc8-7a34-4baf-856c-23c0e9a21743" />
  
- SSH jail status
 <img width="1843" height="221" alt="fail2ban-ssh-status" src="https://github.com/user-attachments/assets/ea5c48bc-1bb4-486c-afc6-c1f5706d08cb" />
 
- Attacker IP banned
<img width="1843" height="221" alt="attacker-banned" src="https://github.com/user-attachments/assets/f9c93b69-5ad5-45f4-9abd-a0adc2fb7424" />
  

## 🔗 Connect

**Author:** Alex Ojo
Cybersecurity Student | SOC Analyst Trainee

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue)](https://linkedin.com/in/alex-o-ojo-ab9252185)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black)](https://github.com/alexojocyber)
