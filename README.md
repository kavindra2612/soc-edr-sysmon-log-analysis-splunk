# 🛡️ SOC EDR Monitoring Dashboard using Splunk

## 📌 Project Overview

This project demonstrates a **SOC (Security Operations Center) Monitoring Dashboard**
built using **Splunk Enterprise** and **Sysmon logs** on Windows Server 2019.

The goal of this project is to simulate real-world SOC monitoring use cases such as:

- Process Creation Monitoring
- Suspicious PowerShell Detection
- Network Connections Monitoring
- Port Scan Detection
- DNS Query Monitoring
- File Creation Monitoring

This project helps in understanding how SOC analysts investigate endpoint activity using SIEM.

---

## 🏗️ Lab Setup

| Component | Details |
|------------|----------|
| SIEM | Splunk Enterprise 10.x |
| Log Source | Sysmon |
| OS | Windows Server 2019 (VMware) |
| Index Used | edr |
| Log Type | Microsoft-Windows-Sysmon/Operational |

---

# 🔍 Detection Use Cases & Queries

---

## 1️⃣ Process Creation Monitoring

**Event ID 1 – Process Creation**
<h2> Process Creation Detection</h2>
<img src="screenshots/Process Creation Detection.png" width="700">

```spl
index=edr EventCode=1
| stats count by Image
| sort -count
```
📌 This query shows the most executed processes in the system.

2️⃣ Suspicious PowerShell Execution Detection
<h2> Suspicious PowerShell Execution</h2>
<img src="screenshots/Suspicious PowerShell Execution.png" width="700">

```spl
index=edr EventCode=1 Image="*powershell*"
| table _time Image CommandLine ParentImage
```
📌 Used to detect potentially suspicious PowerShell activity.

3️⃣ Network Connections Monitoring
<h2>Network Connections Monitoring</h2>
<img src="screenshots/Network Connections Monitoring.png" width="700">

```spl
Event ID 3 – Network Connection

index=edr EventCode=3
| stats count by DestinationIp
| sort -count
```
📌 Displays outbound network connections.

4️⃣ Horizontal Port Scan Detection
<h2> Horizontal Port Scan Detection</h2>
<img src="screenshots/Horizontal Port Scan Detection.png" width="700">

```spl
index=edr EventCode=3
| stats dc(DestinationPort) as unique_ports by SourceIp
| where unique_ports > 10
```
📌 Detects hosts scanning multiple ports (Port Scanning Behavior).

5️⃣ DNS Monitoring

Event ID 22 – DNS Query
<h2> DNS Monitoring</h2>
<img src="screenshots/DNS Monitoring.png" width="700">

```spl
index=edr EventCode=22
| stats count by QueryName
| sort -count
```
📌 Monitors DNS queries to detect suspicious domains.

6️⃣ File Creation Monitoring

Event ID 11 – File Create

<h2> File Creation Monitoring</h2>
<img src="screenshots/File Creation Monitoring.png" width="700">


```spl
index=edr EventCode=11
| stats count by TargetFilename
| sort -count
```
📌 Detects newly created files in the system.

## 📊 Dashboard Overview

This dashboard provides real-time monitoring of endpoint activity.

<h2>📊 Dashboard Overview</h2>
<img src="screenshots/Dashboard.png" width="700">


🎯 Skills Demonstrated

## Splunk SPL Query Writing

- Sysmon Log Analysis

- Threat Hunting

- Port Scan Detection Logic

- PowerShell Monitoring

- SOC Use Case Development

- Dashboard Creation

## 🚀 Project Outcome

This project simulates a real-world SOC analyst workflow:

- Log ingestion

- Log parsing

- Detection engineering

- Dashboard visualization

- Threat investigation

 ## Author

## - Kavindra Patel
SOC & Cybersecurity Enthusiast
