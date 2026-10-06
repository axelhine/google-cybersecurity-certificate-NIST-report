# Incident Report Analysis: ICMP Flood DoS Attack (NIST CSF)

An incident analysis and security improvement plan for a denial-of-service (DoS) attack, organized around the five functions of the **NIST Cybersecurity Framework (CSF)**.

> Completed as part of the Google Cybersecurity Professional Certificate portfolio.
> **[📄 Read the full incident report (PDF)](reports/Incident%20report%20analysis%20NIST.pdf)**

---

## Scenario

A multimedia company (web design, graphic design, and social media marketing for small businesses) suffered a DoS attack that disrupted its internal network for about two hours. A flood of ICMP packets overwhelmed network services, and normal internal traffic could not reach any network resources.

The investigation found that a malicious actor sent an ICMP ping flood through an **unconfigured firewall**, which allowed the attack to succeed.

---

## Incident Summary

| Attribute | Details |
| :--- | :--- |
| **Organization** | Multimedia company serving small businesses |
| **Attack type** | ICMP flood (Denial of Service) |
| **Root cause** | Unconfigured firewall allowed the flood into the network |
| **Impact** | ~2 hours of internal network service disruption |
| **Immediate response** | Blocked incoming ICMP packets, took non-critical services offline, restored critical services |

### Controls Implemented After the Attack

- Firewall rule to rate-limit incoming ICMP packets
- Source IP address verification on the firewall to catch spoofed ICMP traffic
- Network monitoring software to detect abnormal traffic patterns
- IDS/IPS system to filter some ICMP traffic based on suspicious characteristics

---

## NIST CSF Analysis

Each section separates what the team **did** from what this analysis **recommends**.

### 1. Identify
- **Finding:** The attack was an ICMP flood, a form of DoS that overwhelms a system with ICMP packets and shuts down network operations.

### 2. Protect
- **Implemented:** ICMP rate limiting on the firewall and source IP verification.
- **Recommended:**
  - Extend rate limiting and filtering beyond ICMP. The network could still be vulnerable to other floods, such as SYN floods, without similar limits.
  - Apply port filtering to block unused ports and reduce unwanted traffic.
  - Extend the IDS/IPS to cover network traffic as a whole, not just ICMP.
- **Assessment:** The response shows a reactive security posture. The organization needs a proactive posture against attack types beyond the one that occurred.

### 3. Detect
- **Implemented:** Network monitoring software and an IDS/IPS, both added after the attack.
- **Recommended:**
  - Add a SIEM to filter and prioritize alerts by severity. No SIEM was mentioned in the incident.
  - Link the IDS/IPS to the SIEM if that has not already been done.
  - Use Wireshark and/or `tcpdump` to inspect traffic and log data directly, and connect them to the SIEM for more well-rounded monitoring.

### 4. Respond
- **Implemented:** The incident management team contained the attack by blocking incoming ICMP packets and taking non-critical services offline. The cybersecurity team then investigated and traced the attack vector to the unconfigured firewall.
- **Recommended:** Establish procedures to communicate incident status clearly to internal IT staff and to affected end users during an active outage.

### 5. Recover
- **Implemented:** Critical network services were restored once the ICMP flood was mitigated and safety controls were in place.
- **Recommended:**
  - Continuously update recovery procedures so affected assets and data are brought back online without reintroducing vulnerabilities.
  - Maintain clear restoration updates and communication channels with IT personnel and end users to confirm when normal operations have resumed.

---

## Key Takeaways

- **Reactive to proactive:** Blocking packets after an attack hits stops the immediate damage. Long-term security depends on continuous monitoring, rate limiting, and correct firewall configuration in place ahead of time.
- **Technical to strategic:** The NIST CSF connects technical incident response to strategic risk management, so lessons learned feed directly into future identification, protection, detection, response, and recovery.

---

## Skills Demonstrated

- **Incident analysis:** Identifying the attack type and root cause, and evaluating the containment actions taken
- **Network security:** Firewall configuration, ICMP rate limiting, source IP verification, port filtering, and SYN flood awareness
- **Detection and monitoring:** IDS/IPS, SIEM integration, and packet analysis with Wireshark and `tcpdump`
- **Framework alignment:** Applying the NIST CSF (Identify, Protect, Detect, Respond, Recover) to a real-world style incident
- **Communication:** Recommending internal and external incident communication procedures
