# Week 1 - Network Fundamentals & Lab Setup

This document summarizes the key artifacts and skills demonstrated during the first week of the project, focusing on **networking fundamentals**, **virtual lab environment setup**, and **system administration**.

---

## 1. Core Networking Skills

### Subnetting Mastery
- **Artifact:** [30 Timed Subnetting Problems](https://github.com/RezaAramjou/subnetting-cheatsheet/blob/main/examples/timed_problems.md)
- **Description:** A set of 30 progressively difficult IPv4 subnetting problems were solved against a timer to demonstrate both accuracy and speed. The average completion time was approximately **26 seconds per problem**, proving a high level of proficiency.

### Packet Analysis
- **Artifact:** [HTTP Packet Analysis Report](https://github.com/RezaAramjou/labs/blob/main/pcaps/week1-analysis.md)
- **Description:** A live HTTP session was captured using `tcpdump`. The resulting `.pcap` file was analyzed to identify and document the key stages of the connection: the **TCP three-way handshake**, the **HTTP GET request**, and the **server's 200 OK response**. The report also details the secure methodology used to transfer evidence files from the analysis VM to the host machine.

---

## 2. Lab Environment & System Administration

### Virtualization Setup
- **Artifact:** [Snapshot Metadata Log](https://github.com/RezaAramjou/labs/blob/main/virtualbox/snapshots_meta.md)
- **Description:** A standardized lab environment was established using **VirtualBox** with **Ubuntu** and **Kali Linux VMs**. A formal snapshot policy was created to ensure a consistent and recoverable state for all lab work.

### Linux Server Hardening
- **Artifact:** [Ubuntu Server Hardening Report](https://github.com/RezaAramjou/labs/blob/main/linux-admin/user-hardening.md)
- **Description:** A base Ubuntu Server VM was hardened according to security best practices. This included:
  - Creating a new administrative user
  - Enforcing SSH key-only authentication
  - Disabling root login
  - Disabling password authentication
  - Configuring the **UFW firewall**

### GNS3 Network Simulation
- **Artifact:** [GNS3 Troubleshooting & Resolution Report](https://github.com/RezaAramjou/labs/blob/main/gns3/day-06-troubleshooting-report.md)
- **Description:** This report documents a deep-dive troubleshooting session that arose while attempting to set up a GNS3 routing lab. The process involved diagnosing and resolving **host-level package management conflicts (`dkms`)**, a cascade of **GNS3-VirtualBox integration bugs**, and flaws in the **GNS3 GUI**. The exercise demonstrates advanced diagnostic skills, persistence, and the ability to pivot to a more stable architectural solution (the **GNS3 VM**).
