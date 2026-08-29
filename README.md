<div align="center">

# 🛡️ Linux Security & Network Analysis Toolkit

**A modular Bash-based suite for network diagnostics, security hardening, forensic collection, threat detection, and real-time monitoring — with a live web dashboard.**

[![Bash](https://img.shields.io/badge/Shell-Bash_5.x-4EAA25?logo=gnubash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Python](https://img.shields.io/badge/Dashboard-Python_3.8+-3776AB?logo=python&logoColor=white)](https://python.org)
[![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?logo=linux&logoColor=black)](https://kernel.org)
[![Distro Agnostic](https://img.shields.io/badge/Distro-Agnostic-blue?logo=linuxcontainers&logoColor=white)](#requirements)
[![License](https://img.shields.io/badge/License-MIT-lightgrey)](#)
[![Maintained](https://img.shields.io/badge/Maintained-Yes-brightgreen)](#)

<br>

<img src="https://img.shields.io/badge/Modules-10-orange" alt="modules"/> <img src="https://img.shields.io/badge/Network%20Lab%20Tools-12-orange" alt="network lab"/> <img src="https://img.shields.io/badge/Tools%20Hub-11-orange" alt="tools hub"/> <img src="https://img.shields.io/badge/Dashboard-Live-success" alt="dashboard"/>

</div>

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Project Structure](#-project-structure)
- [Features](#-features)
- [Quick Start](#-quick-start)
- [Security Modules Reference](#-security-modules-reference)
- [Network Lab Reference](#-network-lab-reference)
- [Tools Hub Reference](#-tools-hub-reference)
- [Dashboard](#-dashboard)
- [Configuration](#-configuration)
- [Output & Logs](#-output--logs)
- [Requirements](#-requirements)
- [Security Notes](#-security-notes)
- [Author](#-author)

---

## 🔎 Overview

The **Linux Security & Network Analysis Toolkit** is a collection of Bash scripts and tools designed to automate common network analysis, security auditing, threat detection, forensic, and offensive/defensive tooling tasks on Linux systems. Every execution is logged with timestamps, and results are surfaced through an interactive web dashboard with live tailing, full-text search, and real-time system resource monitoring.

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                 🛡️ LINUX SECURITY & NETWORK ANALYSIS TOOLKIT                 ║
║                                                                              ║
╚══════════════════════════════════════╦═══════════════════════════════════════╝
                                       │
                                       ▼
╔══════════════════════════════════════════════════════════════════════════════╗
║                                 🚀 run.sh                                    ║
║                        Unified Entry Point • Main Menu                       ║
╚══════════════════════════════════════╦═══════════════════════════════════════╝
                                       │
             ┌─────────────────────────┼─────────────────────────┐
             │                         │                         │
             ▼                         ▼                         ▼
┌──────────────────────┐    ┌──────────────────────┐    ┌──────────────────────┐
│   🧩 MODULES         │    │   🧪 NETWORK LAB     │    │   🧰 TOOLS HUB       │
│                      │    │                      │    │                      │
│  Security Operations │    │  Learning & Analysis │    │  Security Tooling    │
│                      │    │                      │    │  DFIR & Assessment   │
├──────────────────────┤    ├──────────────────────┤    ├──────────────────────┤
│ • Analysis           │    │ • Diagnostics        │    │ • DFIR               │
│ • Forensics          │    │ • Networking         │    │ • Network Analysis   │
│ • Reconnaissance     │    │ • Security           │    │ • Reverse Engineering│
│ • System Security    │    │ • Protocols          │    │ • SOC Integration    │
│ • Threat Detection   │    │ • Hardening          │    │ • Static Analysis    │
│                      │    │ • Wireless Security  │    │ • Threat Intelligence│
└───────────┬──────────┘    └──────────┬───────────┘    │ • Vulnerability Scan │
            │                          │                │ • Web Security       │
            │                          │                └───────────┬──────────┘
            │                          │                            │
            └──────────────────────────┼────────────────────────────┘
                                       │
                                       ▼
                         ┌───────────────────────────┐
                         │     📊 DASHBOARD          │
                         │                           │
                         │  Live Web UI • HTTP API   │
                         │  Monitoring • Visibility  │
                         └─────────────┬─────────────┘
                                       │
                                       ▼
                  ╔═══════════════════════════════════════╗
                  ║       📝 LOGGING & ARTIFACTS          ║
                  ║                                       ║
                  ║   logs/              output/          ║
                  ║   ─────────          ─────────        ║
                  ║   JSON Logs          Scan Results     ║
                  ║   Audit Trails       Reports          ║
                  ║   Timestamps         Evidence         ║
                  ╚═══════════════════════════════════════╝


                         🔧 SHARED FOUNDATION
                                  │
              ┌───────────────────┼───────────────────┐
              ▼                   ▼                   ▼
       ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
       │ config/     │     │ lib/        │     │ install.sh  │
       │             │     │             │     │             │
       │ Global      │     │ Colors      │     │ Multi-distro│
       │ Settings    │     │ Functions   │     │ Dependency  │
       │             │     │ Logging     │     │ Installer   │
       └─────────────┘     │ Bootstrap   │     └─────────────┘
                           │ Wireshark   │
                           │ Permissions │
                           └─────────────┘
```

---

## 🗂️ Project Structure

```
networking_cybersecurity/
├── 🚀 run.sh                              # Main entry point
├── 📦 install.sh                          # Dependency installer (multi-distro)
├── 📖 README.md
|
├── ⚙️ config/
│   └── settings.conf                   # Global configuration
|
├── 🧱 lib/
│   ├── colors.sh                       # Terminal colour definitions
│   ├── functions.sh                    # Shared utility functions
│   ├── init.sh                         # Library bootstrap
│   ├── logging.sh                      # Structured JSON + audit logging
│   └── setup_wireshark_permissions.sh  # Non-root packet capture setup
|
├── 🧩 modules/
│   ├── run_modules.sh                  # Module menu & execution handler
│   ├── analysis/
│   │   ├── cloud_exposure_audit.sh
│   │   ├── detect_suspicious_net_linux.sh
│   │   └── log_analysis.sh
|   |
│   ├── forensics/
│   │   ├── forensic_collect.sh
│   │   └── system_info.sh
|   |
│   ├── reconnaissance/
│   │   └── web_recon.sh
|   |
│   ├── system_security/
│   │   └── secure_system.sh
|   |
│   └── threat_detection/
│       ├── data_exfil_detect.sh
│       ├── lateral_movement_detect.sh
│       └── malware_analysis.sh
|
├── 🧪 network_lab/
│   ├── network_lab.sh                  # Network Lab controller
│   ├── diagnostics/
│   │   ├── ip_addressing.sh
│   │   └── packet_analysis.sh
│   ├── networking/
│   │   ├── core_protocols.sh
│   │   ├── network_hardening.sh
│   │   ├── networking_basics.sh
│   │   ├── network_master.sh
│   │   ├── network_tools.sh
│   │   └── switching_routing.sh
│   ├── security/
│   │   ├── firewall_ids.sh
│   │   ├── security_fundamentals.sh
│   │   ├── threat_intelligence.sh
│   │   └── wireless_security.sh
│   └── output/
|
├── 🧰 tools/
│   ├── run_tool.sh                     # Tools Hub menu & execution handler
│   ├── configs/
│   │   ├── kubehunter.conf
│   │   ├── openvas.conf
│   │   ├── semgrep_rules.yaml
│   │   └── snort.conf
│   ├── dfir/
│   │   ├── iris_ir.sh                  # IRIS incident-response case sync
│   │   └── thehive_case.sh             # TheHive case management
│   ├── network_analysis/
│   │   └── wireshark.sh                # Wireshark/tshark capture helper
│   ├── reverse_engineering/
│   │   └── ghidra_launcher.sh          # Ghidra headless/GUI launcher
│   ├── soc_platform/
│   │   └── securityonion_integration.sh
│   ├── static_analysis/
│   │   └── semgrep_scan.sh             # Semgrep static analysis
│   ├── threat_intelligence/
│   │   ├── misp_lookup.sh              # MISP IOC lookups
│   │   └── opencti_lookup.sh           # OpenCTI lookups
│   ├── vulnerability_scanning/
│   │   └── kubehunter_scan.sh          # kube-hunter Kubernetes scan
│   └── web_security/
│       └── burpsuite_scan.sh           # Burp Suite automation hook
|
├── 📊 dashboard/
│   ├── start_dashboard.sh
│   ├── server.py                       # Python HTTP API server
│   ├── index.html                      # Dashboard frontend
│   ├── app.js                          # Dashboard JS logic
│   └── style.css                       # Dashboard styles
|
├── 📝 logs/                                # Auto-generated timestamped logs
└── 📦 output/                              # Script output artifacts
```

---

## ✨ Features

### 🔐 Security Modules

| Module | Description |
|---|---|
| 🔍 **Suspicious Network Detection** | Scans active connections for anomalous ports, foreign IPs, and unexpected listeners |
| 🔒 **System Hardening** | Applies firewall rules, disables unused services, locks down SSH, enforces password policies |
| 💻 **System Inventory** | Collects OS version, hardware, users, running services, open ports, and disk info |
| 🕵️ **Forensic Collection** | Captures volatile data — processes, connections, ARP cache, login history, cron jobs |
| 🌐 **Web Recon** | Passive and active reconnaissance including DNS, headers, and directory enumeration |
| 🦠 **Malware Analysis** | Static and dynamic analysis of suspicious files and processes |
| 🔀 **Lateral Movement Detection** | Analyses authentication logs for lateral movement indicators |
| 📋 **Log Analysis** | Parses system logs for threat indicators and anomalies |
| ☁️ **Cloud Exposure Audit** | Probes cloud metadata services for misconfigurations and exposure |
| 📤 **Data Exfiltration Detection** | Scans for data exfiltration patterns in network traffic and logs |

### 🌐 Network Lab

| Tool | Description |
|---|---|
| 🌐 **Network Tools** | Interfaces, ping, traceroute, DNS lookup, port scanning |
| 📡 **Core Protocols** | Analyse TCP/UDP, HTTP, DNS, ICMP in real-time |
| 🔢 **IP Addressing** | Subnetting, CIDR breakdown, NAT, ARP |
| 📦 **Packet Analysis** | Headers, Wireshark filters, PCAP |
| 🗺️ **Network Master** | Comprehensive suite — discovery, scanning, bandwidth, latency |
| 📖 **Networking Basics** | OSI model, TCP/IP, switching guided diagnostics |
| 🔀 **Switching & Routing** | VLANs, MAC tables, RIP/OSPF/BGP |
| 🔐 **Security Fundamentals** | RSA/ECC key gen, AES encryption, SHA hashing, digital signatures |
| 📶 **Wireless Security** | WiFi standards, WPA3, attack vectors |
| 🧱 **Firewall & IDS/IPS** | iptables, nftables, Snort configuration |
| 🛡️ **Network Hardening** | SSH hardening, VPN, Zero Trust |
| 🧠 **Threat Intelligence** | OSINT, CVE lookup, MITRE ATT&CK |

### 🧰 Tools Hub

| Tool | Description |
|---|---|
| 🕸️ **Wireshark / tshark** | Guided packet capture with non-root permission setup |
| 🧬 **Ghidra Launcher** | Headless or GUI reverse-engineering workflows |
| 🧪 **Semgrep Scan** | Static application security testing against custom rule sets |
| ☸️ **kube-hunter Scan** | Kubernetes cluster vulnerability scanning |
| 🕷️ **Burp Suite Automation** | Hooks into Burp for web app security scans |
| 🗞️ **MISP / OpenCTI Lookup** | Threat-intel IOC enrichment via API |
| 🚨 **Security Onion Integration** | SOC platform status, alert, and hunt commands |
| 🧯 **TheHive / IRIS Case Sync** | Push findings straight into DFIR case management |

### 📊 Dashboard

| Feature | Description |
|---|---|
| 📊 **Live Stats** | Total runs, success/warning/fail counts with animated counters |
| 📈 **Metrics** | Success rate ring, average duration, category breakdown chart |
| 🖥️ **System Resources** | Real-time CPU, Memory, Disk, Network usage — updates every 5 seconds |
| ⚠️ **Alerts** | Configurable warn/critical thresholds with optional email notifications |
| 📁 **Log Viewer** | In-browser log viewer with live tail (3-second polling) |
| 🔎 **Full-Text Search** | Search across all log files with match highlighting |
| 📤 **Export** | Download a full plain-text report of all stats, history, and files |

---

### 🧩 Underlying System Commands

The toolkit's scripts wrap standard Linux CLI tools rather than reinventing them. Helper utilities like `grep`, `awk`, `sed`, `find`, `cat` are omitted below for brevity:

| Category                                                                                                            | Commands                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | What it does                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Interface & Link Configuration**                                                                                  | `ip` (addr/link/route/neigh/-s link/-6 route), `ifconfig`, `ethtool`, `iw`, `iwconfig`, `nmcli`, `arp`, `rfkill`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Configures and inspects network interfaces, IP addresses, routes, neighbors/ARP entries, link statistics, Ethernet and Wi-Fi settings, NetworkManager connections, and radio devices.                                                                                                                            |
| **DNS**                                                                                                             | `dig`, `nslookup`, `host`, `whois`, `resolvectl`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Queries DNS records and resolvers, performs hostname lookups, retrieves domain registration information, and manages or inspects system DNS resolution.                                                                                                                                                          |
| **Connectivity / Path Diagnostics**                                                                                 | `ping`, `traceroute`, `tracepath`, `mtr`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Tests network reachability, latency, packet loss, MTU behavior, and the route packets take to a destination.                                                                                                                                                                                                     |
| **Socket / Connection State**                                                                                       | `ss`, `netstat`, `lsof`, `conntrack`, `nc`/`netcat`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Inspects listening ports, active sockets and connections, open files associated with processes, connection-tracking state, and performs basic TCP/UDP connectivity operations.                                                                                                                                   |
| **Packet Capture & Analysis**                                                                                       | `tcpdump`, `tshark`, `wireshark`, `capinfos`, `editcap`, `mergecap`, `hexdump`, `xxd`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Captures, inspects, analyzes, edits, merges, and displays network packet data and binary content.                                                                                                                                                                                                                |
| **Port / Service Scanning**                                                                                         | `nmap`, `masscan`, `hping3`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Discovers hosts and services, scans ports, performs high-speed Internet-scale scanning, and crafts or tests custom TCP/IP packets.                                                                                                                                                                               |
| **Web Recon & Vulnerability Scanning**                                                                              | `whatweb`, `httprobe`, `gowitness`, `nikto`, `gobuster`, `curl`, `wget`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Identifies web technologies, probes HTTP services, captures website screenshots, checks for common web server issues, discovers hidden content, and retrieves web resources.                                                                                                                                     |
| **TLS/SSL**                                                                                                         | `openssl` (s_client, x509, dgst, enc, req, rsa, ec, ecparam, genrsa, rsautl/pkeyutl), `sslscan`, `sslyze`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Tests and manages TLS/SSL connections, certificates, cryptographic hashes, encryption, keys, CSRs, and TLS configuration/security.                                                                                                                                                                               |
| **Firewall / Packet Filtering**                                                                                     | `iptables`, `ip6tables`, `nft`, `ufw`, `firewall-cmd`, `ipset`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Configures packet-filtering rules, IPv4/IPv6 firewalls, firewall policies, zones, and IP address sets.                                                                                                                                                                                                           |
| **NAT / Routing / Kernel Params**                                                                                   | `iptables -t nat`, `ip route`, `sysctl` (e.g. `net.ipv4.ip_forward`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Configures network address translation, routing tables, IP forwarding, and other networking-related kernel parameters.                                                                                                                                                                                           |
| **SSH**                                                                                                             | `ssh`, `sshd`, `ssh-keygen`, `scp`, `sftp`, `fail2ban-client`, `sshguard`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Provides secure remote access and file transfer, manages SSH keys and the SSH server, and helps protect services against repeated authentication attacks.                                                                                                                                                        |
| **SMB / NFS / RPC**                                                                                                 | `smbclient`, `showmount`, `enum4linux`, `rpcinfo`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Inspects and interacts with SMB shares, NFS exports, Samba/Windows information, and RPC services.                                                                                                                                                                                                                |
| **VPN**                                                                                                             | `wg` (WireGuard), `openvpn`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Configures, manages, and connects VPN tunnels using WireGuard or OpenVPN.                                                                                                                                                                                                                                        |
| **Kubernetes**                                                                                                      | `kubectl`, `kube-hunter`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Manages Kubernetes clusters and workloads and assesses Kubernetes environments for common security weaknesses.                                                                                                                                                                                                   |
| **Malware Analysis / Reverse Engineering**                                                                          | `yara`, `ghidraRun`/`analyzeHeadless`, `strings`, `objdump`, `readelf`, `ssdeep`, `ldd`, `file`, `chkrootkit`, `rkhunter`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Identifies and analyzes malware and binaries, extracts strings and metadata, disassembles executables, checks dependencies, performs fuzzy hashing, and looks for possible rootkits.                                                                                                                             |
| **Process / Kernel Forensics**                                                                                      | `lsmod`, `modinfo`, `busctl`, `dbus-send`, `ptrace_scope` (via `sysctl`/`/proc`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Inspects loaded kernel modules and their metadata, interacts with D-Bus services, and examines or controls process tracing restrictions.                                                                                                                                                                         |
| **Auditing / Logging**                                                                                              | `journalctl`, `auditctl`, `ausearch`, `dmesg`, `last`, `lastb`, `lastlog`, `w`, `who`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Views system and kernel logs, configures and searches Linux auditing events, and examines user login, session, and activity history.                                                                                                                                                                             |
| **IDS/IPS & SIEM**                                                                                                  | `snort`, `suricata`, `zeek`/`bro`, Security Onion (`so-status`, `so-restart`, `so-hunt`, `so-alert-log`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Detects and analyzes suspicious network activity, generates security telemetry, and manages or investigates Security Onion monitoring and alerting components.                                                                                                                                                   |
| **Static Analysis**                                                                                                 | `semgrep`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Performs pattern-based static code analysis to identify bugs, insecure code patterns, and policy violations.                                                                                                                                                                                                     |
| **Web App Security**                                                                                                | `burpsuite`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Provides an intercepting proxy and tools for testing and analyzing web application security.                                                                                                                                                                                                                     |
| **Threat Intel (via API/curl)**                                                                                     | MISP, OpenCTI, TheHive, IRIS — all accessed via `curl` + API tokens, no dedicated CLI tool                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Integrates with threat intelligence, case management, incident response, and analysis platforms through their HTTP APIs.                                                                                                                                                                                         |
| **Detection Targets** (searched for on disk/in-process or referenced in documentation, not executed by the toolkit) | `iodine`, `dns2tcp`, `dnscat`, `nstx`, `dnstt`, `ptunnel`, `ptunnel-ng`, `icmptunnel`, `icmpsh`, `mimikatz`, `pypykatz`, `lazagne`, `impacket-secretsdump`, `hashcat`, `john`, `hydra`, `medusa`, `ncrack`, `crackmapexec`, `bloodhound`, `ldapdomaindump`, `kerbrute`, Metasploit/`msfconsole`/meterpreter, Empire, Cobalt Strike, Sliver, Nighthawk, Havoc, Merlin, Covenant, Mythic, `pwncat`, `mitmproxy`, `charles`, `fiddler`, `sslstrip`, `sqlmap`, `nuclei`, `chisel`, `ligolo`/`ligolo-ng`, `frp`/`frpc`/`frps`, `proxychains`, `3proxy`, `tor`, `i2p`/`i2pd`, `hcxdumptool`, `hcxtools`, `aircrack-ng` suite (`airmon-ng`, `airodump-ng`, `aireplay-ng`), `reaver`, `bully`, `pixiewps`, `wpscan`, `kismet`, `bettercap`, `pkexec`, `doas` | These are detection indicators and references for tunneling, credential access, password attacks, reconnaissance, exploitation, command-and-control, proxying, wireless attacks, privilege escalation, and other security-relevant tooling; they are searched for or referenced but not executed by the toolkit. |

> **Note:** On Debian/Ubuntu, tools installed to `/usr/sbin` or `/sbin` (e.g. `ifconfig`, `ethtool`, `iw`, `iwconfig`, `arp`, `rfkill`) aren't on a regular user's `PATH` by default, even after `install.sh` installs them. Run the toolkit with `sudo`, or add `export PATH="$PATH:/usr/sbin:/sbin"` to your shell profile.

---

## 🚀 Quick Start

**1. Install dependencies**

```bash
chmod +x install.sh
sudo ./install.sh
```

**2. Run the interactive menu**

```bash
chmod +x run.sh
sudo ./run.sh
```

**3. Launch the dashboard**

```bash
cd dashboard
python3 server.py
# Open http://localhost:8000
```

> 💡 **Optional:** Install `psutil` for live system resource monitoring:
> ```bash
> pip install psutil --break-system-packages
> ```

---

## 🔐 Security Modules Reference

All modules are invoked through `run.sh → Run Security Modules` or directly. Each execution produces a timestamped log in `logs/` and any output artifacts in `output/`.

| Script | Purpose | Timeout |
|---|---|---|
| `analysis/detect_suspicious_net_linux.sh` | Flags unusual ports, unexpected listeners, and connections to foreign IPs outside a whitelist using `ss`, `netstat`, and `/proc/net` | 800s |
| `system_security/secure_system.sh` | Configures `ufw`/`iptables`, hardens `sshd_config`, disables unneeded services, sets password aging via `chage`/`pam` | 200s |
| `forensics/system_info.sh` | OS, kernel, hostname, uptime, CPU, memory, disk, running services, open ports, local accounts and sudo privileges | 200s |
| `forensics/forensic_collect.sh` | Captures processes, connections, ARP cache, routing table, cron jobs (all users), login history, auth log tail, loaded kernel modules | 400s |
| `reconnaissance/web_recon.sh` | DNS enumeration (A/MX/TXT/NS), HTTP header analysis, directory/path enumeration, robots.txt/sitemap discovery — prompts for a target | 200s |
| `threat_detection/malware_analysis.sh` | Static and dynamic analysis of suspicious files and running processes | 600s |
| `threat_detection/lateral_movement_detect.sh` | Analyses auth logs for unusual login chains, privilege escalation patterns, and credential abuse | 300s |
| `analysis/log_analysis.sh` | Parses system logs for failed auth attempts, sudo abuse, unusual cron activity, and more | 300s |
| `analysis/cloud_exposure_audit.sh` | Probes AWS/GCP/Azure metadata services for misconfigurations and unintended exposure | 200s |
| `threat_detection/data_exfil_detect.sh` | Scans active connections and log history for data exfiltration patterns | 300s |

> All module timeouts are configurable via `config/settings.conf` (`TIMEOUT_<script_name>`), overriding the built-in defaults.

---

## 🌐 Network Lab Reference

Accessible via `run.sh → Network Lab`. All tools are interactive and run locally — no data leaves the machine.

**Diagnostics & Live Analysis**
- **Network Tools** — Ping sweep, traceroute, DNS lookup, Whois, port scan via `nmap`
- **Core Protocols** — Live TCP/UDP, HTTP, DNS, ICMP analysis
- **IP Addressing** — Subnet calculator, CIDR breakdown, NAT/ARP inspection
- **Packet Analysis** — Header dissection, Wireshark filter builder, PCAP review

**Education & Reference**
- **Network Master** — All networking topics in one comprehensive module
- **Networking Basics** — OSI model walkthroughs, TCP/IP stack, switching concepts
- **Switching & Routing** — VLAN info, routing table analysis, RIP/OSPF/BGP reference
- **Security Fundamentals** — Hands-on cryptography demos, all run locally:

```
┌─────────────────────────────────────┐
│  Security Fundamentals              │
├─────────────────────────────────────┤
│  1. RSA key generation & encrypt    │
│  2. ECC key pair generation         │
│  3. AES-256 encryption/decryption   │
│  4. SHA-256 / SHA-512 hashing       │
│  5. Digital signature (sign/verify) │
│  6. File integrity check            │
└─────────────────────────────────────┘
```

**Advanced Security**
- **Wireless Security** — WiFi standards, WPA2/WPA3, common attack vectors
- **Firewall & IDS/IPS** — iptables/nftables rule building, Snort rule reference
- **Network Hardening** — SSH lockdown, VPN setup, Zero Trust principles
- **Threat Intelligence** — OSINT techniques, CVE lookup, MITRE ATT&CK framework

**Automation**
- **Run All Network Lab Modules** — executes all twelve tools sequentially, logging each run

---

## 🧰 Tools Hub Reference

Accessible via `run.sh → Tools Hub`. This is the integration layer for third-party and specialist security tools.

| Category | Script | Purpose |
|---|---|---|
| Network Analysis | `network_analysis/wireshark.sh` | Guided capture setup, including non-root permission configuration via `lib/setup_wireshark_permissions.sh` |
| Reverse Engineering | `reverse_engineering/ghidra_launcher.sh` | Launches Ghidra in headless or GUI mode for binary analysis |
| Static Analysis | `static_analysis/semgrep_scan.sh` | Runs Semgrep against `configs/semgrep_rules.yaml` |
| Vulnerability Scanning | `vulnerability_scanning/kubehunter_scan.sh` | Runs kube-hunter against a Kubernetes cluster using `configs/kubehunter.conf` |
| Web Security | `web_security/burpsuite_scan.sh` | Automates Burp Suite scan workflows |
| Threat Intelligence | `threat_intelligence/misp_lookup.sh`, `threat_intelligence/opencti_lookup.sh` | IOC enrichment against MISP and OpenCTI via API |
| SOC Platform | `soc_platform/securityonion_integration.sh` | Wraps Security Onion status/alert/hunt commands |
| DFIR | `dfir/iris_ir.sh`, `dfir/thehive_case.sh` | Pushes findings and evidence into IRIS or TheHive case management |

Tool-specific defaults (rule sets, scan targets, API endpoints) live in `tools/configs/`.

---

## 📊 Dashboard

The dashboard is a self-contained Python HTTP server + vanilla JS frontend. **No npm, no build step required.**

**Starting**

```bash
# Via run.sh menu (option 3: View Dashboard)
chmod +x run.sh
sudo ./run.sh

# Or directly
cd dashboard && python3 server.py

# Custom port
DASHBOARD_PORT=9090 python3 server.py
```

Then open **http://localhost:8000** in your browser. Use option **7** in the main menu to stop the dashboard cleanly.

**Email Notifications (SMTP)**

```bash
export SMTP_HOST=smtp.gmail.com
export SMTP_PORT=587
export SMTP_USER=you@gmail.com
export SMTP_PASS=your_app_password

python3 server.py
```

Use the **⚠ Alerts** button in the dashboard to set CPU/Memory/Disk thresholds and enable automatic email alerts.

**API Endpoints**

| Endpoint | Method | Description |
|---|---|---|
| `/api/dashboard-data` | GET | Full dashboard payload (logs, outputs, history, stats) |
| `/api/metrics` | GET | Success rate, avg duration, category breakdown, disk usage |
| `/api/system-stats` | GET | Live CPU, Memory, Disk, Network (requires `psutil`) |
| `/api/file` | GET | Serve a log or output file (`?dir=logs&name=file.log`) |
| `/api/tail` | GET | Last N lines + mtime for live tailing |
| `/api/search` | GET | Full-text search across all log files |
| `/api/notify-email` | POST | Send an email notification (requires SMTP config) |
| `/api/alert-settings` | GET/POST | Read or update alert thresholds |

---

## ⚙️ Configuration

All global defaults live in `config/settings.conf` and are sourced by `run.sh` before any other file. Key settings:

```bash
# Dashboard
DASHBOARD_PORT=8000
DASHBOARD_ORIGIN=*

# Logging
LOG_LEVEL=INFO
MAX_LOG_FILES=100
LOG_RETENTION_DAYS=30
ENABLE_AUDIT_LOG=true
ENABLE_JSON_LOGS=true
JSON_LOG_MAX_KB=4096

# Script execution
DEFAULT_SCRIPT_TIMEOUT=200

# Security
CONFIRM_RISK_LEVEL=high

# Alert thresholds (dashboard system monitor)
ALERT_CPU_WARN=70
ALERT_CPU_CRIT=90
ALERT_MEM_WARN=75
ALERT_MEM_CRIT=90
ALERT_DISK_WARN=80
ALERT_DISK_CRIT=95
```

Override any value by exporting an environment variable before running (`export LOG_LEVEL=DEBUG`), or by creating a git-ignored `config/settings.local.conf`, which is sourced last and always wins:

```bash
echo 'config/settings.local.conf' >> .gitignore
```

Shared library functions are in `lib/functions.sh` and `lib/logging.sh` — source them in any custom script:

```bash
source "$(dirname "$0")/../lib/functions.sh"
source "$(dirname "$0")/../lib/colors.sh"
```

---

## 📁 Output & Logs

**Log Files**

Every script run creates a timestamped log at `logs/<script>_<YYYYMMDD_HHMMSS>.log`. Logs capture: start time, full command output, exit code, and completion timestamp. When `ENABLE_JSON_LOGS` is enabled, structured `.jsonl` files are also written for the dashboard's rich metadata; a global append-only audit trail is kept at `logs/toolkit.jsonl` when `ENABLE_AUDIT_LOG` is set. The dashboard parses these to determine run status (success / warning / error) and duration.

**Output Files**

Scripts that produce artifacts write to `output/<category>_<timestamp>/`. Example for `security_fundamentals.sh`:

```
output/security_20260310_144125/
├── rsa_private.pem / rsa_public.pem
├── ecc_private.pem / ecc_public.pem
├── rsa_plain.txt / rsa_cipher.bin / rsa_decrypted.txt
├── aes_data.txt / aes_data.enc / aes_data.dec
├── doc_to_sign.txt / doc.sig
└── doc.sha256 / integrity_test.sha256
```

---

## 📋 Requirements

**System**

| Requirement | Notes |
|---|---|
| Linux | Debian/Ubuntu, Arch/Manjaro, RHEL/Fedora/CentOS, openSUSE, Alpine, Void — all supported, distro auto-detected |
| Bash 5.x | `bash --version` |
| Python 3.8+ | For dashboard server |
| Core tools | `ss`, `ip`, `dig`, `curl`, `openssl` |
| `nmap` | Optional — for port scanning features |
| `psutil` | Optional — `pip install psutil --break-system-packages` — for dashboard system stats |
| `semgrep`, `gvm-tools` | Optional — installed automatically via pip where available, used by Tools Hub |

**Permissions**

Some modules require elevated privileges:

```bash
sudo ./run.sh

# Or run individual scripts directly
sudo ./modules/system_security/secure_system.sh
sudo ./modules/forensics/forensic_collect.sh
```

`install.sh` also configures non-root packet-capture permissions via `lib/setup_wireshark_permissions.sh`.

---

## 🛡️ Security Notes

- All scripts operate **locally** — no data is sent to external services unless you explicitly configure SMTP, or use the Threat Intelligence / SOC Platform / DFIR tools in `tools/`, which call external APIs (MISP, OpenCTI, TheHive, IRIS) using your own credentials.
- The dashboard server binds to `localhost` by default. **Do not expose it publicly without authentication.**
- Forensic and hardening scripts should be reviewed before running in production environments.
- RSA/ECC keys and encrypted files generated by `security_fundamentals.sh` are for **demonstration purposes only**.
- The **Run All Security Modules** and **Run All Network Lab Modules** options execute every script sequentially — allow significant time and review timeouts in `config/settings.conf`.
- Vulnerability scanning, credential-attack, and exploitation-adjacent tools in `tools/` should only be run against systems you own or are explicitly authorized to test.

---

## 👤 Author

**Hitesh Mondal** — Developer & Cybersecurity Enthusiast

Focus areas: Networking • System Security • DevOps • Cloud Infrastructure
