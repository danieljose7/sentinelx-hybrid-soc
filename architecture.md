# SentinelX Architecture & Telemetry Pipeline

## 1. Environment Topology
The local SOC lab is built using Vagrant and VirtualBox, isolating the environment from the host machine. It consists of:
- **win11 (Endpoint):** A Windows 11 virtual machine acting as the primary target, configured to generate robust endpoint security telemetry.
- **logger (SIEM):** An Ubuntu virtual machine acting as the centralized logging server, running Splunk Enterprise.

## 2. Telemetry Pipeline (On-Premises)
Our core log forwarding mechanism relies on the Splunk Universal Forwarder.
1. **Log Generation:** The Windows 11 endpoint generates Windows Security Event Logs and Sysmon Operational logs.
2. **Collection:** The Universal Forwarder (running as a background service on `win11`) reads these local event channels.
3. **Transmission:** The forwarder transmits the collected logs over TCP port 9997 to the Splunk Logger VM.
4. **Indexing & Parsing:** Splunk parses the incoming XML/text streams, extracting fields like `AccountName`, `CommandLine`, and `EventCode`, and stores them in the `main` index.
5. **Detection:** Scheduled SPL cron jobs run against the `main` index every 5 minutes to identify malicious patterns and trigger alerts.

## 3. Phase 2 Expansion (Cloud)
*Currently in development.* AWS CloudTrail logs will be ingested via the Splunk Add-on for AWS to provide hybrid cloud visibility and IAM threat detection.
