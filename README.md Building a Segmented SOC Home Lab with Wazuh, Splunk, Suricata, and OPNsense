Building a Segmented SOC Home Lab with Wazuh, Splunk, Suricata, and OPNsense

Project Objective
Techologies Used

Network Architecture

The objective of this lab is to build a segmented cybersecurity environment capable of:

- Simulating attacks from a Kali Linux attacker machine
- Detecting malicious activity using Suricata IDS/IPS on OPNsense
- Centralizing and monitoring logs with Wazuh and Splunk
- Reproducing a realistic SOC (Security Operations Center) environment

---

Technologies Used

- VMware Workstation
- OPNsense
- Suricata IDS/IPS
- Wazuh
- Splunk
- Kali Linux
- DVWA
- Ubuntu Server

---

Network Architecture

The lab environment was segmented into two virtual networks:

Internal / Monitoring Network

Contains:

- DVWA vulnerable server
- Wazuh manager
- Splunk server
- OPNsense LAN interface

Attacker Network

Contains:

- Kali Linux attacker VM
- OPNsense OPT1 interface

OPNsense routes traffic between both networks, forcing all attack traffic through the firewall and IDS/IPS engine.

This improved:

- network visibility
- IDS inspection
- traffic monitoring
- threat detection

---

Key Technologies Configured

OPNsense

- Firewall routing
- Network segmentation
- Inter-network traffic control

Suricata IDS/IPS

- IDS mode enabled
- ET Open rulesets configured
- EVE JSON logging enabled
- Alert generation validated

Wazuh

- Agent deployment
- Security event monitoring
- Log visibility validation

Splunk

- Remote syslog forwarding
- Security log centralization
- SIEM monitoring

---

Important Networking Discovery

A critical issue was identified during testing:

When Kali Linux and DVWA were placed on the same subnet, attack traffic bypassed OPNsense and Suricata could not properly inspect internal scans.

Resolution

The solution implemented was:

- separating attacker and victim networks
- forcing all traffic through OPNsense routing

This provided practical understanding of:

- network segmentation
- IDS visibility
- routing
- firewall inspection
- Layer 2 switching

---

Planned Improvements

- Full Suricata → Wazuh integration
- Splunk dashboards
- Nmap alert validation
- Threat hunting exercises
- Red Team / Blue Team simulations
- Detection engineering practice

---

Skills Practiced

- VMware virtual networking
- Network segmentation
- Firewall configuration
- OPNsense administration
- IDS/IPS deployment
- Suricata configuration
- Linux networking
- Wazuh integration
- Splunk log forwarding
- Traffic inspection
- SOC architecture concepts

---

Conclusion

This project successfully created a realistic segmented SOC home lab environment capable of:

- attack simulation
- firewall and IDS inspection
- centralized logging
- SIEM integration
- IDS alert generation

This lab provides strong hands-on experience for:

- SOC Analyst roles
- Blue Team operations
- Security+ preparation
- Detection engineering
- cybersecurity portfolio development
