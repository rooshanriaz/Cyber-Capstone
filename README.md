# Cyber Security Capstone Lab

## Overview

This repository contains a comprehensive seven-phase cybersecurity capstone project designed to simulate the complete enterprise security lifecycle. The project combines offensive security, threat modeling, detection engineering, purple team operations, and digital forensics into a unified security program.

The objective was to demonstrate how modern organizations identify, assess, detect, respond to, and recover from cyber threats while aligning security controls with industry frameworks such as:

* MITRE ATT&CK
* OWASP ASVS
* OWASP Top 10
* NIST SP 800-53
* STRIDE
* DREAD

---

## Project Phases

### Phase 1 — Offensive Security Assessment

Performed a full penetration test against a vulnerable banking application environment to identify and validate exploitable weaknesses.

### Phase 2 — Threat Modeling & Risk Assessment

Developed Data Flow Diagrams (DFDs), conducted STRIDE analysis, and prioritized risks using the DREAD framework.

### Phase 3 — Adversary Emulation

Executed a structured attack campaign mapped directly to MITRE ATT&CK techniques while maintaining operational security boundaries.

### Phase 4 — Detection Engineering

Designed and implemented custom detection logic using Wazuh SIEM, Sysmon, and Atomic Red Team.

### Phase 5 — Purple Team Operations

Conducted collaborative attack simulations to validate defensive controls and improve detection coverage.

### Phase 6 — Detection Validation & Security Metrics

Measured detection effectiveness, alert quality, and defensive readiness against simulated adversary behaviors.

### Phase 7 — Digital Forensics & Incident Response

Performed memory and disk forensic investigations to reconstruct attacker activities and identify Indicators of Compromise (IOCs).

---

## Technologies Used

### Offensive Security

* Kali Linux
* Nmap
* Burp Suite
* Gobuster
* SQLMap
* Nikto

### Threat Modeling

* STRIDE
* DREAD
* OWASP ASVS
* NIST 800-53

### Detection Engineering

* Wazuh
* Sysmon
* Atomic Red Team
* Sigma Concepts

### Purple Teaming

* Havoc C2
* MITRE ATT&CK
* Wazuh SIEM

### DFIR

* Volatility 3
* Autopsy
* Sleuth Kit
* FTK Imager

---

## Key Outcomes

* Conducted full attack-chain simulations from reconnaissance to incident response.
* Developed custom detections for ATT&CK-aligned techniques.
* Built threat models and risk assessments for vulnerable applications.
* Performed forensic investigations of post-compromise environments.
* Demonstrated offensive and defensive security integration through purple team exercises.

---

## Disclaimer

All activities were performed in isolated laboratory environments with explicit authorization. No testing was conducted against production systems or third-party infrastructure.
