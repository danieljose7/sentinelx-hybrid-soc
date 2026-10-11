# MITRE ATT&CK Mapping

This document maps the custom detection logic engineered in the SentinelX lab to the MITRE ATT&CK framework.

## Detection 1: Brute Force Authentication
* **Tactic:** Credential Access
* **Technique:** T1110 - Brute Force
* **Data Source:** Windows Security Event Log (Event ID 4625)
* **Description:** Detects multiple failed authentication attempts to identify potential password guessing or brute-force attacks against local accounts. Machine accounts (ending in `$`) are filtered to reduce false positives.

## Detection 2: Suspicious PowerShell Execution
* **Tactic:** Execution
* **Technique:** T1059.001 - Command and Scripting Interpreter: PowerShell
* **Data Source:** Sysmon (Event ID 1 - Process Creation)
* **Description:** Monitors command-line arguments for known evasion and execution flags such as `bypass`, `encodedcommand`, and `iex`. This identifies Living-off-the-Land (LotL) techniques used to circumvent execution policies.

## Detection 3: Privileged Account Activity
* **Tactic:** Privilege Escalation / Persistence
* **Technique:** T1078.003 - Valid Accounts: Local Accounts
* **Data Source:** Windows Security Event Log (Event ID 4672 - Special privileges assigned to new logon)
* **Description:** Identifies non-SYSTEM accounts invoking administrative privileges upon logon. A spike in these events for standard users acts as a high-fidelity indicator of lateral movement or unauthorized privilege use.
