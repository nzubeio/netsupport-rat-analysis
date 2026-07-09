# NetSupport Manager RAT Malware Traffic Analysis

This project documents my investigation of a simulated NetSupport RAT infection using Wireshark. By analyzing a packet capture (PCAP), I identified the compromised host, traced its communication with a command-and-control (C2) server,  indicators of compromise (IOCs) with threat intelligence, and reconstructed the attack timeline to understand the malware's behavior.

## Investigation Objectives

The primary objectives of this investigation were to:
- Identify the compromised host withing the network traffic.
- Determine the malware's command-and-control (C2) infrastructure.
- Identify indicators of compromise(IOCs).
- Reconstruct the attack timeline from the packet capture.
- Recommend remediation actions based on the findings.

## Environment

| Item | Value |
|------ | ------|
|Analysis Tool | Wireshark |
| Evidence File | `2026-02-28-traffic-analysis.pcap` |
| Malware Family | NetSupport Manager RAT |
| Victim Host | `10.2.28.88` |
| Primary C2 Server | `45.131.214.85` |
| Protocols Observed | TCP, HTTP, TLS 1.2 |
| Operating System | Windows |

## Victim Identification

The investigation began by identifying the internal host responsible for suspicious outbound network activity. Filtering the packet capture for the encrypted HTTPS traffic (`tcp.port == 443`) revealed repeated communication between the interanl workstation `10.2.28.88` and the external IP address `13.89.179.9`.

At this stage of the investigation, the HTTPS communication alone was not sufficient to conclude that the host was compromised, as encrypted traffic over port 443 is common in enterprise environments. However, the repeated outbound conncections established the system as the primary host requiring further investigation. 


**Finding:** Internal host **10.2.28.88** was identified as the primary system of interest and selected for deeper investigation.


![Victim Identification](image.png)


*Figure 1. Initial traffic analysis showing the internal host (10.2.28.88) communicating with the external IP address (13.89.179.9) over TCP port 443. At this stage, encrypted HTTPS traffic alone was not sufficient to confirm compromise but identified the primary system requiring further investigation.*
  
