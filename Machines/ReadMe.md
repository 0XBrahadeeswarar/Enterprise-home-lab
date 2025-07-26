#  Machines Overview

This folder contains all virtual machines used in the **Enterprise Home Lab** project. Each subfolder includes setup documentation and configuration files for a specific machine.

##  Machine List

###  `dc-server/`
- **OS**: Windows Server 2025
- **Role**: Domain Controller (AD DS, DNS, DHCP)
- **Purpose**: Central Active Directory server for the lab
- **Docs**: `walkthrough.md`, `config.md`

---

###  `windows-client/`
- **OS**: Windows 11 
- **Role**: Workstation client
- **Purpose**: Simulates a typical domain-joined corporate endpoint
- **Docs**: `walkthrough.md`, `config.md`,  

---

###  `ubuntu-client/`
- **OS**: Ubuntu 22.04
- **Role**: Linux client joined to AD
- **Purpose**: Tests domain join, Winbind/Kerberos authentication from Linux
- **Docs**: `walkthrough.md`, `config.md`, `issues.md`

---

###  `email-server/` 
- **OS**: TBD (likely Ubuntu/Debian)
- **Role**: Email server (Postfix/Dovecot)
- **Purpose**: Internal mail for domain users

---

###  `security-server/`
- **OS**: TBD
- **Role**: Security tools server (Wazuh, Suricata, etc.)
- **Purpose**: Blue Team monitoring, threat detection

---

>  Each machine folder includes:
> - `walkthrough.md` – Step-by-step setup guide  
> - `config.md` – Key configuration details  
> - `issues.md` – Troubleshooting notes (if needed)
