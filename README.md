# Enterprise-Infrastructure-Security-Assessment-Lab
An isolated enterprise cyber range for Active Directory adversary simulation and detection engineering. Features a pfSense firewall, Windows Server 2022 AD infrastructure, a Windows 11 target workstation, and a Kali Linux attack platform, with centralized security monitoring powered by a Security Onion SIEM.

## 🧠 Why I Built This
I put this lab together to bridge the gap between knowing cybersecurity theory and actually seeing it play out on a live wire. Instead of just reading about Active Directory exploits or firewall configurations, I wanted a safe, hands-on environment where I could execute real-world attacks from a Kali machine, watch how a Windows domain collapses, and—most importantly—figure out exactly how to detect and stop those actions using enterprise-grade monitoring.

---

## 🏗️ Network Architecture & Setup
To simulate a true corporate environment, the network is strictly segmented to keep things realistic and safe:
*   **The Gateway:** A `pfSense` firewall acts as the backbone, handling all routing and isolating the lab networks from my home LAN.
*   **The Domain:** `Windows Server 2022` handles Active Directory, identity management, and domain policies, mimicking a standard corporate network.
*   **The Targets:** A `Windows 11` workstation represents a typical employee endpoint waiting to be targeted.
*   **The Watcher:** `Security Onion` sits quietly on a separate management/monitoring segment, sniffing traffic and gathering telemetry across the entire environment.

---

## ⚡ What I Use This Lab For

### 🔴 Red Team / Offensive Testing
*   **Initial Access & Poisoning:** Simulating LLMNR/NBT-NS poisoning attacks.
*   **Credential Hunting:** Dumping LSASS memory and pulling password hashes to practice offline cracking.
*   **Active Directory Exploitation:** Executing classic domain attacks like Kerberoasting, AS-REP Roasting, and Pass-the-Hash.
*   **Lateral Movement:** Moving from the compromised Windows 11 endpoint up to the Domain Controller.

### 🔵 Blue Team / Defensive Monitoring & Detection
*   **Telemetry Generation:** Setting up `Sysmon` and Windows Event Forwarding to ensure every process creation, network connection, and registry tweak gets logged.
*   **SIEM Ingestion:** Sending host logs and network traffic through Zeek and Suricata into `Security Onion` for a single pane of glass view.
*   **Rule Writing (Detection Engineering):** Writing custom alerts to catch anomalies, like an unusual process spawning out of `cmd.exe` or sudden spike in Kerberos ticket requests.
*   **Threat Hunting:** Digging through raw telemetry to map out a complete timeline of an attack after running a script from Kali.

---

## 🚀 Lessons Learned & Key Takeaways
*   **Visibility is Everything:** An attack that looks completely invisible on a standard Windows machine stands out like a sore thumb once you map your Sysmon logs correctly to your SIEM.
*   **Default Settings Aren't Enough:** Out-of-the-box Active Directory configs are incredibly fragile. Hardening policies (like disabling LLMNR) makes an attacker's life significantly harder.
*   **The Loop:** Cyber defense isn't a one-time setup. The best way to learn is a continuous cycle: attack, analyze the logs, build a defense, and try the attack again.
