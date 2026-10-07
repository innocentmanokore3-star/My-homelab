# Dual-Node Purple Team Cyber Range

## Project Overview
This repository documents offensive attack simulations, defensive log analysis, and SIEM detection engineering across a persistent dual-node cyber range.

---

## Homelab Hardware & Network Architecture

### Physical Infrastructure
* **Attack Host (Red Team):** Dell Latitude 3190 running bare-metal **Kali Linux**.
* **Hypervisor Host (Blue Team):** ASUS VivoBook Go 15 (AMD Ryzen 5, 16 GB RAM) running **Oracle VirtualBox**.

### Virtual Machines & Roles

| VM Name | Role / Operating System | IP Address | Services / Monitoring |
| :--- | :--- | :--- | :--- |
| **`wazuh-server`** | Central SIEM (Manager & Indexer) | `10.184.230.144` | OpenSearch Dashboard & Log Parsing |
| **`metasploitable3-ub1404`** | Vulnerable Target Endpoint | Dynamic / Host-Only | SSH, ProFTPD, Wazuh Agent |

---

## Weekly Activity Logs
* [Week 1: Cyber Range Setup, Reconnaissance & SSH Brute-Force Telemetry](docs/week1.md)
