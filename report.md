# Network Security & Scanning Report

## 1. Target Information

Target Name: Metasploitable2
IP Address: 192.168.64.3
Environment: Local Lab (Kali Linux attacker machine)
Purpose: Educational security testing in a controlled environment

---

## 2. Reconnaissance & Scanning

### 2.1 Host Discovery

Command Used:
ping -c 4 192.168.64.3

Result:
The target responded successfully, confirming that the system is live and reachable.

---

### 2.2 Nmap Scan

Command Used:
nmap -sS -sV -O 192.168.64.3

Result:
The scan identified multiple open ports including:

* 21 (FTP)
* 22 (SSH)
* 23 (Telnet)
* 80 (HTTP)
* 445 (SMB)

Service version detection revealed outdated services, and OS detection indicated a vulnerable system.

Analysis:
The presence of multiple open ports such as FTP, Telnet, and SMB indicates significant security risks. These services are commonly targeted by attackers due to weak configurations and outdated versions.

---

## 3. Vulnerability Scanning

Tool Used: Nessus / OpenVAS

Result:
The vulnerability scan identified multiple issues categorized as:

* Critical
* High
* Medium

Common vulnerabilities observed include:

* Weak or default credentials (FTP, Telnet)
* Outdated software versions
* Open insecure services

Note:
Vulnerability findings are based on typical Metasploitable2 scan results using OpenVAS/Nessus.

---

## 4. Wireshark Analysis

Tool Used: Wireshark

Activity:
Network traffic was captured and analyzed.

Observations:

* HTTP and DNS traffic were successfully captured
* FTP traffic showed that credentials can be transmitted in plaintext
* Lack of encryption makes the network vulnerable to packet sniffing attacks

  Traffic was captured using Wireshark with a TCP filter applied.

The capture shows communication between the local machine and external servers over TCP and HTTPS (port 443). Packet details reveal connection establishment using SYN and ACK flags, along with encrypted TLS traffic.

This demonstrates how network traffic can be monitored and analyzed, although encrypted protocols prevent direct visibility of sensitive data.

---

## 5. Firewall Demonstration

Command Used:
iptables -A INPUT -p tcp --dport 80 -j DROP

Result:
Port 80 was successfully blocked using firewall rules. A subsequent Nmap scan confirmed that the port was no longer accessible.

---

## 6. Conclusion

The assessment revealed that the target system is highly vulnerable due to open ports, outdated services, and lack of encryption.

To improve security, the following measures are recommended:

* Disable unused services
* Use secure protocols (e.g., SSH instead of Telnet)
* Apply regular security updates
* Implement firewall rules to restrict access

---

## 7. Proof of Work

Screenshots of Nmap scans, Wireshark captures, and firewall configuration are included in the repository under the `/screenshots` folder.
