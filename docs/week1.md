# Week 1: Cyber Range Build, Agent Enrollment & Threat Simulation

## Portfolio Overview
Established a dual-node cyber range to test end-to-end security operations. The setup pairs a physical Red Team attack host with a virtualized Blue Team target monitored by a central SIEM platform.

---

## 1. Lab Architecture & Node Inventory

* **Red Team Host (Attacker):** Dell Latitude 3190 (Kali Linux)
* **Blue Team Hypervisor:** ASUS VivoBook Go 15 (VirtualBox)
* **SIEM Manager:** `wazuh-server` (`10.184.230.144`)
* **Monitored Endpoint Agent:** `metasploitable3-ub1404` (`agent.id: 000`)

---

## 2. Execution Phases & Log Telemetry

### Phase 1: Endpoint Agent Enrollment & Port Monitoring
* Configured the `ossec` decoder on the Wazuh agent to monitor system network state.
* **Evidence:** Collected active socket states (`netstat listening ports`) confirming active listeners on SSH (22), HTTPS (443), and FTP (21).

### Phase 2: Service Reconnaissance & Brute-Force Attack
* Conducted initial service probing against ProFTPD (`ProFTPD: FTP session opened`).
* Executed automated credential guessing against SSH services.

### Phase 3: Telemetry Ingestion & Metric Breakdown

| Telemetry Metric | Event Count | SOC Analysis & Context |
| :--- | :--- | :--- |
| **Total Ingested Events** | 8,317 | Total system, network, and security events recorded. |
| **Authentication Failures** | 5,177 | Massive spike caused by automated brute-force execution. |
| **Authentication Successes**| 11 | Successful session establishments captured. |
| **Monitored Endpoint Agent** | `metasploitable3-ub1404` | Verified active telemetry pipeline from target VM. |

---

## 3. Incident Findings & MITRE ATT&CK Mapping
* **T1110 - Brute Force:** Ingested 5,177 failed logon events within a 30-minute window, firing Wazuh alert levels 5 through 10.
* **T1021.004 - Remote Services (SSH):** Identified SSH as the targeted protocol vector.
* **T1078 - Valid Accounts:** Flagged 11 successful logons following failure spikes, highlighting potential compromised credentials.

---

## 4. Key Takeaways & Defense Lessons
1. **Telemetry Verification:** Inspecting raw JSON/Table documents in Wazuh ensures that decoder rules accurately parse field names like `decoder.name: ossec` and `rule.description`.
2. **Detection Rule Tuning:** High volumes of failed authentications followed by sudden successful logons serve as a high-confidence Indicator of Compromise (IoC) for security operations.

---
![Wazuh Threat Hunting Overview](images/wazuh-overview.png)
![Raw Log JSON Inspection](images/raw-log-json.png)
