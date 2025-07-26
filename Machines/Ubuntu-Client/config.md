# Configuration Summary – Ubuntu Client

This document explains the configuration files used to successfully connect the Ubuntu client to the Windows Domain Controller (`CORP.HOME-LABS-DC.COM`).

---

## 1. `/etc/samba/smb.conf`

This config file enables the Ubuntu client to communicate with the Active Directory domain using Samba.

Key points:
- `realm = CORP.HOME-LABS-DC.COM`: Your AD domain name.
- `workgroup = CORP`: Your NetBIOS domain name.
- `security = ads`: Tells Samba to act as an AD client.
- `winbind` settings: Allow listing AD users and groups using `wbinfo` and `getent`.

📄 File: [`smb.conf`](./smb.conf)

---

## 2. `/etc/nsswitch.conf`

This tells Ubuntu to use `winbind` to resolve users and groups from the domain, allowing domain logins and UID/GID mapping.

📄 File: [`nsswitch.conf`](./nsswitch.conf)

---

## 3. `/etc/resolv.conf`

Configured manually to ensure DNS queries are sent to the Windows DC for domain name resolution. This is critical for Kerberos and domain joining.

- Nameserver: `10.0.0.5` (your DC)

📄 File: [`resolv.conf`](./resolv.conf)

---

## 4. Static IP Settings

We manually configured:
- IP: `10.0.0.101`
- Gateway: `10.0.0.1`
- Subnet: `255.255.255.0`
- DNS: `10.0.0.5` (DC)

📄 File: [`static-ip-settings.txt`](./static-ip-settings.txt)

---

## 5. Domain Join Commands

These commands were used during the setup:
- `net ads join -U Administrator`
- `systemctl restart winbind` *(must be done after joining to authenticate users)*

📄 File: [`join-domain-commands.txt`](./join-domain-commands.txt)

---

## 6. Services

We ensured the following services were enabled and restarted:
- `smbd`
- `nmbd`
- `winbind`

📄 File: [`winbind-service.txt`](./winbind-service.txt)

---

