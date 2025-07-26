#  Windows DC Server - Walkthrough

This walkthrough covers the installation and configuration of the Windows Server 2022 VM used as the Domain Controller (DC) in our enterprise-style home lab.

---

## System Configuration

- **OS**: Windows Server 2022 (64-bit)
- **Role**: Domain Controller
- **VM Name**: `Windows-dc-server`
- **Computer Name**: `Windows-dc-server`
- **Hostname**: `DC`
- **Domain**: `corp.home-labs-dc.com`
- **IP Address**: `10.0.0.5`
- **Default Gateway**: `10.0.0.1`
- **DNS**: `127.0.0.1` (self)
- **HDD**: 50 GB
- **Network Adapter**: NAT Network 

---

##  Installation Steps

1. **Create VM in VirtualBox**
   - Name: `Windows-dc-server`
   - Type: Microsoft Windows
   - Version: Windows 2022 (64-bit)
   - RAM: 4096 MB (or higher)
   - HDD: 50 GB
   - Network: NAT Network

2. **Mount ISO and Install**
   - Use Windows Server 2022 ISO.
   - Standard installation.
   - Choose "Desktop Experience"  .
   - Set Administrator password.

---

##  Post-Installation Configuration

1. **Change Computer Name**
   - Set the hostname to `Windows-dc-server`
   - Reboot after rename

2. **Set Static IP**
   - IPv4 Address: `10.0.0.5`
   - Subnet Mask: `255.255.255.0`
   - Gateway: `10.0.0.1`
   - DNS: `10.0.0.5`

---
##  Configure DNS Forwarders

1. Open **DNS Manager** (`Tools > DNS` in Server Manager).
2. Right-click on the server name > **Properties**.
3. Go to the **Forwarders** tab.
4. Click **Edit** and add:
   - `8.8.8.8` (Google DNS)
   - `1.1.1.1` (Cloudflare DNS - optional)
5. Click **OK** to save.

-- This allows your clients and the DC itself to resolve external domain names like `microsoft.com` using your internal DNS server with external forwarders.

---

##  Promote to Domain Controller

1. **Open Server Manager > Add Roles and Features**
2. Select:
   - **Role-Based or Feature-Based Installation**
   - Select local server
   - Add **Active Directory Domain Services (AD DS)**
   - Also install DNS ,DHCP when prompted
3. After install, click **Promote this server to a domain controller**
4. Choose **Add a new forest**
   - Domain: `corp.home-labs-dc.com`
5. Set DSRM password
6. Proceed with defaults, wait for reboot

---