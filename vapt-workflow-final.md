# Neo-VAPT: Final Advanced Workflow (2024-2025)

This workflow combines industry-standard methodologies (PTES, OWASP, NIST) with modern attack scenarios for Active Directory and Cloud environments, optimized for execution by the Neo-VAPT agent on Kali Linux.

---

## Phase 1: Planning & Reconnaissance (Intel Gathering)
*Goal: Map the attack surface and identify high-value targets.*

### 1.1 External Recon (Web/Network)
- **Tools:** `nmap`, `sublist3r`, `amass`, `theHarvester`.
- **Action:** Identify IP ranges, subdomains, open ports, and service banners.
- **Scenario:** Map all assets for a target domain `example.com`.

### 1.2 Internal Recon (AD/Identity)
- **Tools:** `BloodHound-python`, `Adidnsdump`, `Responder`.
- **Action:** Passive discovery of AD objects, mapping trust relationships, and LLMNR/NBT-NS poisoning.
- **Scenario:** Identifying the shortest path to Domain Admin from a low-priv user.

---

## Phase 2: Vulnerability Assessment (Deep Inspection)
*Goal: Identify exploitable flaws while minimizing noise.*

### 2.1 Web Application Testing
- **Tools:** `Burp Suite` (Scanner/Repeater/Collaborator), `nikto`, `sqlmap`, `wfuzz`.
- **Action:** Test for OWASP Top 10 (Injection, Broken Access Control, etc.). Use Burp Collaborator for blind OOB vulnerabilities.

### 2.2 Infrastructure & Cloud Assessment
- **Tools:** `searchsploit`, `openvas`, `checkov` (if repo access), `prowler` (for Cloud).
- **Action:** Cross-reference service versions with Exploit-DB; check for misconfigured S3 buckets or IAM roles.

---

## Phase 3: Exploitation (Precision Strikes)
*Goal: Verify vulnerabilities and gain initial access.*

### 3.1 Network/Service Exploitation
- **Tools:** `Metasploit` (`msfconsole`), `hydra` (for brute force), `searchsploit`.
- **Action:** Execute precise exploit modules against verified vulnerable services.

### 3.2 Identity & AD Exploitation
- **Tools:** `impacket-scripts` (Kerberoasting/AS-REP Roasting), `crackmapexec`, `Responder`.
- **Action:** Capture hashes, request service tickets, or exploit AD CS misconfigurations (ESC1-ESC8).

---

## Phase 4: Post-Exploitation & Lateral Movement
*Goal: Maintain access, escalate privileges, and demonstrate impact.*

### 4.1 Privilege Escalation
- **Tools:** `LinPEAS`, `WinPEAS`, `Mimikatz`.
- **Action:** Run local enumeration scripts to find weak permissions, stored passwords, or kernel exploits.

### 4.2 Lateral Movement
- **Tools:** `evil-winrm`, `psexec.py`, `wmiexec.py`.
- **Action:** Use captured hashes or tickets to move to higher-value systems in the network.

---

## Phase 5: Reporting & Remediation
*Goal: Communicate findings and provide actionable fixes.*

- **Action:** Compile a Markdown report including:
  - **Executive Summary:** Overall risk posture.
  - **Technical Findings:** Commands used, evidence (screenshots/logs), and CVSS rating.
  - **Remediation:** Step-by-step guidance to fix each vulnerability.

---

## Operational Guardrails (Agent Specific)
1. **Tool Budgeting:** Max 15 tools loaded. Use `kali_unload` frequently.
2. **Stealth Mode:** Prefer `nmap -sS` and passive OSINT for initial phases.
3. **Safety First:** No destructive actions (`rm`, `format`, `dd`) without explicit confirmation.
4. **Logging:** Maintain a detailed history of all `execute_command` outputs for final report generation.
