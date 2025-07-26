# Configuration Summary – Windows DC Server

This document explains the key configuration settings applied to the Windows Server 2022 virtual machine used as the Domain Controller.

---

## 🔧 Static IP Configuration

- **IPv4 Address**: `10.0.0.5`
- **Subnet Mask**: `255.255.255.0`
- **Gateway**: `10.0.0.1`
- **DNS**: `10.0.0.5` (self-referencing DNS)

Configured via Control Panel > Network Connections > Ethernet > Properties > IPv4 Settings.

---

## 🌐 DNS Forwarders

Added forwarders in DNS Manager to allow external name resolution:

- `8.8.8.8` (Google)
    -OR-
- `1.1.1.1` (Cloudflare,optional)

> Set in **DNS Manager > Server Properties > Forwarders** tab.

---

##  Active Directory Domain Setup

- **Domain**: `corp.home-labs-dc.com`
- **Forest**: New forest created
- **Hostname**: `Windows-dc-server`

> Done using **Server Manager > Add Roles and Features**, then promoted to a domain controller.

---

##  Roles Installed

- Active Directory Domain Services (AD DS)
- DNS Server
- DHCP Server 

Installed through the **Add Roles and Features Wizard**.

---

