# SentinelX — Hybrid Cloud SOC & Threat Detection Lab

## ?? Project Overview
SentinelX is a custom-built Hybrid SOC (Security Operations Center) environment designed to simulate real-world threat detection, log ingestion, and incident investigation. 

The project demonstrates the complete lifecycle of a SOC alert: from generating endpoint telemetry and shipping logs to a SIEM, to engineering SPL detection queries and mapping alerts to the MITRE ATT&CK framework.

## ??? Technology Stack
* **Infrastructure:** Vagrant, Oracle VirtualBox
* **Endpoints:** Windows 11 (Target), Ubuntu Linux (SIEM Logger)
* **SIEM:** Splunk Enterprise
* **Telemetry:** Windows Security Event Logs, Sysmon (System Monitor)
* **Log Shipper:** Splunk Universal Forwarder

## ?? Telemetry Pipeline (Phase 1 - On-Premises)
1. **Execution:** Controlled adversarial activity (e.g., PowerShell bypass, brute force) is executed on the isolated Windows 11 endpoint.
2. **Collection:** Sysmon and Windows Event logs are captured locally.
3. **Ingestion:** Splunk Universal Forwarder ships logs over TCP 9997 to the Splunk Indexer.
4. **Detection:** Scheduled cron alerts evaluate the `main` index using custom Search Processing Language (SPL).

## ??? Verified Detections (Engineered in SPL)
| Detection Name | Event Source | MITRE ATT&CK Technique |
|---|---|---|
| 1. Brute Force Authentication | WinEventLog:Security (4625) | T1110 - Brute Force |
| 2. Suspicious PowerShell | Sysmon (1) | T1059.001 - PowerShell |
| 3. Privileged Account Activity | WinEventLog:Security (4672) | T1078.003 - Local Accounts |

## ?? Project Roadmap
* **Phase 1:** Core On-Premises SOC & Endpoint Detections (Completed)
* **Phase 2:** AWS CloudTrail Integration & IAM Threat Detections (In Progress)
* **Phase 3:** Automated SOAR Webhooks via Slack/Discord (Planned)
