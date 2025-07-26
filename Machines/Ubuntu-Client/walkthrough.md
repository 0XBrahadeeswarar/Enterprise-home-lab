# Ubuntu Client Integration with Windows Active Directory [samba+winbind](CORP.HOME-LABS-DC.COM)

## 📘 Overview

This walkthrough explains how to configure an Ubuntu 22.04 machine as a domain-joined client under the Windows Server AD domain `CORP.HOME-LABS-DC.COM` (IP: `10.0.0.5`).

---

##  Network Configuration

### Static IP Setup (via GUI)

Ubuntu client configured with:
- **IP Address:** `10.0.0.101`
- **Gateway:** `10.0.0.1`
- **DNS:** `10.0.0.5` (Domain Controller)
- **Subnet Mask:** `255.255.255.0`

---

##  Required Packages

```bash
sudo apt update
sudo apt install -y samba winbind libnss-winbind libpam-winbind krb5-config samba-dsdb-modules samba-vfs-modules
```

##  Kerberos Setup

During prompts:

```
Default realm: CORP.HOME-LABS-DC.COM
```
---

##  Samba Configuration

Backup original:

```bash
sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.org
sudo vi /etc/samba/smb.conf
```

Add the following:

```ini
[global]
   kerberos method = secrets and keytab
   realm = CORP.HOME-LABS-DC.COM
   workgroup = CORP
   security = ads
   template shell = /bin/bash
   winbind enum groups = Yes
   winbind enum users = Yes
   winbind separator = +
   idmap config * : rangesize = 1000000
   idmap config * : range = 1000000-19999999
   idmap config * : backend = autorid
```
###  Overview of smb.conf Configuration

This configuration enables integration with the Active Directory domain. It sets up Kerberos authentication, specifies the domain (`realm`) and workgroup, and ensures domain users and groups are visible on the Ubuntu client. The `autorid` backend automatically maps AD user/group IDs to local IDs, so no manual ID mapping is needed.



---

##  DNS Configuration

Edited directly (instead of Netplan):

```bash
sudo nano /etc/resolv.conf
```

Add:

```ini
nameserver 10.0.0.5
```

>  If overwritten on reboot, consider making `resolv.conf` immutable.

---


---

##  NSS Configuration

Edit `/etc/nsswitch.conf`:

```bash
sudo vi /etc/nsswitch.conf
```

Modify these lines:

```ini
passwd:         files systemd winbind
group:          files systemd winbind
```

---

##  Domain Join

```bash
sudo net ads join -U administrator
```

```bash
sudo systemctl restart winbind

To confirm:

```bash
wbinfo -u
wbinfo -g
```

---

##  Test Domain Users

```bash
su - CORP+janed
```
 >Give credentials to janed and there you go ! You will be successfully get connect to DC 
 >If any issues while configuration --> Check issues.md  



---

