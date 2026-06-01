# CryptoBank Penetration Test & Full System Compromise

## Overview

This lab simulates a real-world external penetration test against a vulnerable banking application environment named **CryptoBank**. The objective was to assess the security posture of the application and underlying infrastructure from the perspective of an unauthenticated attacker and determine the potential business impact of identified vulnerabilities.

The engagement followed a complete penetration testing methodology including reconnaissance, attack surface enumeration, vulnerability discovery, exploitation, post-exploitation analysis, privilege escalation, and remediation planning.

The assessment ultimately resulted in full system compromise through a chain of weaknesses including SQL Injection, information disclosure, credential reuse, insecure development artifacts, and privilege escalation opportunities.

---

# Objectives

The primary objectives of the engagement were:

- Identify exposed services and attack surface.
    
- Discover vulnerabilities within the web application.
    
- Assess authentication and authorization mechanisms.
    
- Validate exploitability of identified weaknesses.
    
- Determine impact on confidentiality, integrity, and availability.
    
- Escalate privileges where possible.
    
- Extract sensitive information to demonstrate business risk.
    
- Produce actionable security recommendations.
    

---

# Assessment Methodology

The assessment was conducted following a structured penetration testing lifecycle.

```text
Reconnaissance
      ↓
Enumeration
      ↓
Vulnerability Discovery
      ↓
Exploitation
      ↓
Post-Exploitation
      ↓
Privilege Escalation
      ↓
Impact Assessment
      ↓
Remediation
```

---

# Target Environment

|Component|Details|
|---|---|
|Platform|CryptoBank VM|
|Operating System|Linux|
|Web Server|Apache 2.4.29|
|Database|MySQL 5.7.29|
|SSH Service|OpenSSH 7.6p1|
|Application|CryptoBank Trading Platform|
|Testing Role|External Unauthenticated Attacker|

---

# Phase 1 – Reconnaissance

## Network Discovery

The engagement began with network reconnaissance to identify reachable services and potential attack vectors.

### Objectives

- Discover live hosts
    
- Enumerate open ports
    
- Identify running services
    
- Determine operating system characteristics
    

### Findings

|Port|Service|Version|
|---|---|---|
|22|SSH|OpenSSH 7.6p1|
|80|HTTP|Apache 2.4.29|

### Security Observations

- Public web application accessible via HTTP.
    
- SSH service exposed externally.
    
- Linux operating system fingerprint identified.
    
- Limited network attack surface but multiple application-layer attack opportunities.
    

---

# Phase 2 – Web Application Enumeration

The web application became the primary attack surface following initial reconnaissance.

## Directory Enumeration

Several directories and resources were identified through content discovery.

### Notable Resources

```text
/info.php
/development/
/trade/
/assets/
/server-status
```

### Security Concerns

- Information disclosure through diagnostic files.
    
- Restricted development resources exposed externally.
    
- Potential administrative functionality accessible through hidden endpoints.
    
- Misconfigured server resources.
    

---

## Application Mapping

The target resolved to a banking application portal named:

```text
CryptoBank Trading Platform
```

### Observed Features

- Authentication portal
    
- Trading functionality
    
- Account management
    
- Loan application services
    
- Balance inquiry services
    

### Attack Surface Identified

|Component|Risk|
|---|---|
|Login Portal|Injection Attacks|
|Development Directory|Information Disclosure|
|PHP Info Page|Technology Disclosure|
|Database Backend|Data Exposure|

---

# Phase 3 – Vulnerability Discovery

## SQL Injection Assessment

The login functionality was selected for further testing due to its interaction with backend databases.

### Vulnerable Endpoint

```text
/trade/login_auth.php
```

### Input Parameters

```text
user
pass
login
```

### Vulnerability Type

```text
Time-Based Blind SQL Injection
```

### Impact

The vulnerability enabled attackers to:

- Enumerate databases
    
- Extract database metadata
    
- Dump application tables
    
- Retrieve sensitive records
    
- Bypass authentication controls
    

---

## Database Enumeration

Following successful exploitation, backend database enumeration was performed.

### Environment Information

|Item|Value|
|---|---|
|DBMS|MySQL|
|Version|5.7.29|
|Current Database|cryptobank|
|Current User|cryptobank@localhost|
|Privileges|DBA|

### Databases Identified

Multiple databases were discovered, with the primary focus placed on:

```text
cryptobank
```

---

# Phase 4 – Sensitive Data Extraction

After confirming database compromise, targeted extraction of high-value information was conducted.

## User Enumeration

The assessment successfully identified:

- Application users
    
- Authentication records
    
- Password hashes
    
- Administrative accounts
    

## Security Impact

Compromise of database contents resulted in:

### Confidentiality Breach

- User account exposure
    
- Credential disclosure
    
- Internal application information leakage
    

### Integrity Risk

- Potential account manipulation
    
- Unauthorized modifications
    

### Availability Risk

- Potential destructive database operations
    

---

# Phase 5 – Authentication Bypass

The extracted credentials enabled further compromise of the environment.

## Attack Chain

```text
SQL Injection
      ↓
Database Enumeration
      ↓
Credential Extraction
      ↓
Credential Validation
      ↓
System Access
```

### Result

Valid credentials were identified and leveraged to obtain access beyond the web application layer.

---

# Phase 6 – Post Exploitation

Following successful access, additional investigation of the host environment was performed.

## Information Disclosure Findings

### Exposed Development Resources

The assessment uncovered development-related resources containing sensitive operational information.

### Backup File Exposure

Accessible backups revealed:

- Source code information
    
- Configuration details
    
- Internal application architecture
    

### Git Repository Exposure

Improperly secured development artifacts exposed repository information useful for further compromise.

---

# Phase 7 – Command Execution Analysis

A development tool containing unsafe functionality was identified.

## Security Issue

Improper input handling enabled command execution capabilities.

### Risk

Successful abuse of this functionality could result in:

- Arbitrary command execution
    
- Host compromise
    
- Remote code execution
    
- Persistence opportunities
    

---

# Phase 8 – Privilege Escalation

The final stage focused on obtaining elevated privileges.

## Apache Solr Assessment

An outdated Apache Solr deployment was identified during host enumeration.

### Security Weakness

The service contained publicly documented vulnerabilities capable of enabling elevated access.

### Impact

Successful exploitation resulted in:

```text
Root-Level Access
```

---

# Attack Chain Summary

```text
External Attacker
        ↓
Reconnaissance
        ↓
Directory Enumeration
        ↓
SQL Injection Discovery
        ↓
Database Enumeration
        ↓
Credential Extraction
        ↓
Authentication Bypass
        ↓
System Access
        ↓
Development Resource Discovery
        ↓
Command Execution
        ↓
Privilege Escalation
        ↓
Root Compromise
```

---

# MITRE ATT&CK Mapping

|Tactic|Technique|
|---|---|
|Reconnaissance|Active Scanning|
|Initial Access|Exploit Public-Facing Application|
|Credential Access|Credentials from Databases|
|Discovery|Service Discovery|
|Discovery|System Information Discovery|
|Lateral Movement|Remote Services|
|Execution|Command and Scripting Interpreter|
|Privilege Escalation|Exploitation for Privilege Escalation|

---

# Security Recommendations

## Application Security

- Implement parameterized SQL queries.
    
- Perform strict server-side input validation.
    
- Deploy secure coding standards.
    
- Conduct regular code reviews.
    

## Authentication

- Enforce MFA.
    
- Eliminate credential reuse.
    
- Implement password complexity requirements.
    

## Infrastructure Security

- Remove exposed development artifacts.
    
- Restrict access to sensitive directories.
    
- Disable unnecessary services.
    

## Monitoring & Detection

- Deploy centralized logging.
    
- Monitor authentication events.
    
- Alert on suspicious database activity.
    
- Implement WAF protections.
    

---

# Lessons Learned

This assessment demonstrated how a single application-layer vulnerability can initiate a complete attack chain leading to full system compromise. The engagement highlighted the importance of secure software development practices, defense-in-depth security controls, credential management, and continuous vulnerability management.

The exercise reinforced the need for organizations to view vulnerabilities not as isolated findings but as interconnected weaknesses that can be chained together by an adversary to achieve significant impact.

---

# Skills Demonstrated

- Penetration Testing
    
- Web Application Security
    
- Vulnerability Assessment
    
- SQL Injection Testing
    
- Attack Surface Analysis
    
- Security Enumeration
    
- Post-Exploitation Analysis
    
- Privilege Escalation Assessment
    
- Risk Assessment
    
- Technical Security Reporting
    
- MITRE ATT&CK Mapping
    
- Security Remediation Planning