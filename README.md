# SOC-Network-Traffic-Investigation-with-Wireshark
Conducted a SOC investigation using Wireshark, Nmap, and Telnet. Identified reconnaissance activity, analyzed packet captures, detected insecure remote access, and produced an incident report with findings and remediation recommendations. Skills: SOC Operations, Threat Detection, Network Security, Wireshark, Nmap.

## Project Overview

This project simulates a real-world Security Operations Center (SOC) investigation.

As a SOC Analyst for Barclays Telco, I investigated suspicious network activity targeting an internal Ubuntu server.

The investigation focused on:

- Network reconnaissance detection
- Port scanning identification
- Telnet traffic analysis
- Packet inspection using Wireshark
- Evidence collection
- Incident documentation

---

## Scenario

Barclays Telco observed unusual network activity against one of its internal systems.

Management requested an investigation to determine:

- Source of activity
- Targeted systems
- Protocols involved
- Evidence of scanning
- Potential security impact

---

## Lab Environment

| System | Role |
|----------|----------|
| Kali Linux | Suspicious Host |
| Ubuntu Server | Internal Target |
| Wireshark | Packet Analysis |
| Nmap | Port Scanning |
| Telnet | Insecure Remote Access |

---

## Lab Topology

Kali Linux
192.168.1.100

↓

Ubuntu Server
192.168.1.102

↓

Port 23 (Telnet)

---

## Investigation Process

### Step 1 – Configure Ubuntu Target

Enabled Telnet service on Ubuntu.

Verified that TCP Port 23 was listening.

### Step 2 – Configure Kali Host

Installed:

- Nmap
- Telnet
- Wireshark

Validated network connectivity.

### Step 3 – Capture Traffic

Started packet capture using Wireshark.

### Step 4 – Generate Reconnaissance Activity

Executed:

```bash
sudo nmap -sS -p 1-100 <target-ip>
```

Executed:

```bash
sudo nmap -sV -p 23 <target-ip>
```

### Step 5 – Generate Telnet Session

```bash
telnet 192.168.1.102 23
```

Executed commands:

```bash
whoami
hostname
pwd
exit
```

### Step 6 – Packet Analysis

Analyzed:

- SYN packets
- SYN/ACK responses
- TCP resets
- Telnet traffic
- TCP streams

---

## Wireshark Filters Used

### Scanning Activity

```text
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

### Open Ports

```text
tcp.flags.syn == 1 && tcp.flags.ack == 1
```

### Closed Ports

```text
tcp.flags.reset == 1
```

### Telnet Traffic

```text
tcp.port == 23
```

### Telnet Session

```text
ip.addr == 192.168.1.100 && ip.addr == 192.168.1.102 && tcp.port == 23
```

---

## Findings

### Suspicious Source

Kali Linux Host

### Target

Ubuntu Internal Server

### Evidence of Reconnaissance

Multiple TCP SYN packets were sent across multiple ports.

### Evidence of Service Enumeration

Port 23 was identified as open.

### Evidence of Telnet Activity

Successful Telnet session observed.

### Security Concern

Telnet transmitted session content in clear text.

### Risk

Potential credential exposure.

---

## Recommendations

- Disable Telnet
- Replace Telnet with SSH
- Restrict remote administration
- Monitor scanning activity
- Implement IDS/IPS controls
- Review firewall rules

---

## Skills Demonstrated

- Security Monitoring
- Threat Detection
- Incident Investigation
- Packet Analysis
- Network Forensics
- SOC Operations
- Wireshark
- Nmap
- Incident Reporting

---

## Screenshots

See screenshots folder.

---

## Author

Palence Konissi

Cybersecurity, Cloud Engineer & Cloud Security Enthusiast

AWS | Security | Terraform
