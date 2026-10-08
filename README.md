# windows-server-az800-home-lab
Hands-on Windows Server 2022 home lab covering Hyper-V, networking, Active Directory, DNS, Group Policy, PowerShell, and AZ-800 administration concepts.
Absolutely. Use this as your **complete `README.md`**. It documents what you have actually completed so far without claiming the labs we haven't done yet.

````markdown
# Windows Server 2022 AZ-800 Home Lab

A hands-on Windows Server 2022 home lab built to develop practical System Administration and Microsoft AZ-800: Administering Windows Server Hybrid Core Infrastructure skills.

The lab focuses on building, configuring, securing, troubleshooting, and documenting a small Windows Server environment using Hyper-V, Active Directory, DNS, Group Policy, networking, and PowerShell.

---

## 🎯 Objectives

The main objectives of this lab are to:

- Build a Windows Server 2022 environment from scratch
- Gain practical experience with Hyper-V
- Configure IPv4 networking and virtual networks
- Deploy Active Directory Domain Services (AD DS)
- Configure and troubleshoot DNS
- Create and manage Active Directory users, groups, and OUs
- Join Windows client machines to a domain
- Configure and troubleshoot Group Policy
- Manage Windows Server using PowerShell
- Practice Windows Server security and administration
- Troubleshoot real-world infrastructure issues
- Build practical skills aligned with the AZ-800 certification
- Document the entire environment as an IT portfolio project

---

# 🖥️ Lab Environment

| Component | Configuration |
|---|---|
| Host Server | Windows Server 2022 |
| Domain Controller | SRV-DC01 |
| Client VM | LAB-WIN10 |
| Virtualization | Hyper-V |
| Virtual Switch | LAB-INTERNAL |
| Domain | lab.local |
| NetBIOS Domain | LAB |
| DNS | Active Directory Integrated DNS |
| Client OS | Windows 10 |
| Server RAM | 8 GB |
| Client VM RAM | 2 GB |
| Client VM CPU | 2 vCPU |
| Client VM Disk | 40 GB |

---

# 🌐 Network Architecture

The lab uses two separate networks.

### Physical Network

```text
Physical Ethernet
      |
      |
192.168.10.0/24
      |
      |
SRV-DC01
192.168.10.1
````

### Hyper-V Internal Lab Network

```text
              SRV-DC01
                 |
        192.168.20.1/24
                 |
          LAB-INTERNAL
          Hyper-V Switch
                 |
        192.168.20.10/24
                 |
            LAB-WIN10
```

### IP Addressing

| Device                       | IP Address    | Subnet Mask | DNS          |
| ---------------------------- | ------------- | ----------- | ------------ |
| SRV-DC01 - Physical Ethernet | 192.168.10.1  | /24         | —            |
| SRV-DC01 - Lab Internal      | 192.168.20.1  | /24         | —            |
| LAB-WIN10                    | 192.168.20.10 | /24         | 192.168.20.1 |

The Windows 10 client does not use a default gateway because the lab is currently focused on internal domain services rather than Internet routing.

---

# 🖥️ Hyper-V

Hyper-V was installed on the Windows Server 2022 host.

A dedicated Hyper-V Internal virtual switch was created:

```text
LAB-INTERNAL
```

The Windows 10 virtual machine is connected to this switch.

### Windows 10 VM

```text
Name: LAB-WIN10
Generation: Generation 2
RAM: 2 GB
CPU: 2 vCPU
Disk: 40 GB
Network: LAB-INTERNAL
```

---

# 🌐 Network Troubleshooting

During the initial configuration, the Windows 10 VM received an APIPA address:

```text
169.254.x.x
```

This indicated that the VM did not have a valid IPv4 configuration on the Hyper-V network.

The Hyper-V internal adapter was then configured with:

```text
192.168.20.1/24
```

The Windows 10 VM was configured with:

```text
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
Default Gateway: None
DNS Server: 192.168.20.1
```

Connectivity was then verified successfully.

Example test:

```cmd
ping 192.168.20.1
```

Result:

```text
0% packet loss
```

---

# 🏢 Active Directory Domain Services

Active Directory Domain Services was installed on `SRV-DC01`.

A new Active Directory forest and domain were created:

```text
Domain: lab.local
NetBIOS: LAB
Domain Controller: SRV-DC01
```

The domain controller also provides DNS services for the lab domain.

---

# 🌐 DNS

DNS was installed as part of the Active Directory deployment.

The Windows 10 client uses the domain controller as its DNS server:

```text
DNS Server: 192.168.20.1
```

DNS resolution was tested using:

```cmd
nslookup lab.local
```

and:

```cmd
nslookup SRV-DC01.lab.local
```

The client was able to resolve the domain and domain controller hostname.

Example:

```text
Name: SRV-DC01.lab.local
Address: 192.168.10.1
```

---

# 🗂️ Active Directory Organizational Units

The following Organizational Units were created:

```text
Users-Lab
Workstations
Servers
IT
Test
```

The `LAB-WIN10` computer account was moved into:

```text
Workstations
```

This allows workstation-specific Group Policy settings to be applied to the client.

---

# 👤 Active Directory Users

A normal domain user account was created:

```text
Username: simphiwe.ngindi
First Name: Simphiwe
Last Name: Ngindi
```

The user was successfully used to log into the Windows 10 domain client.

Domain login:

```text
LAB\simphiwe.ngindi
```

---

# 👥 Active Directory Security Groups

A security group was created:

```text
IT-Admins
```

Configuration:

```text
Group Scope: Global
Group Type: Security
```

The following user was added to the group:

```text
LAB\simphiwe.ngindi
```

Group membership was verified from the Windows 10 client using:

```cmd
whoami /groups
```

The output confirmed membership in:

```text
LAB\IT-Admins
```

This verified that Active Directory authentication and group membership were functioning correctly.

---

# 🔐 Group Policy

A workstation security Group Policy Object was created:

```text
LAB - Workstation Security
```

The GPO was linked to:

```text
Workstations
```

### Configured Policy

The following security setting was configured:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── Security Options

Interactive logon:
Do not display last signed-in
```

The setting was enabled.

---

# ✅ Group Policy Verification

Group Policy was manually refreshed on the Windows 10 client:

```cmd
gpupdate /force
```

The applied policies were then checked using:

```cmd
gpresult /r
```

The output confirmed that the following GPOs were applied:

```text
LAB - Workstation Security
Default Domain Policy
```

This verified that the Windows 10 workstation was successfully receiving Group Policy from the domain.

---

# 🧪 Verification Commands

The following commands have been used during the lab.

### Check IP configuration

```powershell
Get-NetIPAddress -AddressFamily IPv4 |
Select-Object InterfaceAlias,IPAddress,PrefixLength
```

### Test network connectivity

```cmd
ping 192.168.20.1
```

### Test DNS resolution

```cmd
nslookup lab.local
```

```cmd
nslookup SRV-DC01.lab.local
```

### Refresh Group Policy

```cmd
gpupdate /force
```

### View applied Group Policy

```cmd
gpresult /r
```

### View current user and group membership

```cmd
whoami /groups
```

---

# 🛠️ Troubleshooting Lessons

This lab has already involved troubleshooting several common infrastructure problems.

### APIPA Address

The Windows 10 VM initially received an address in the:

```text
169.254.0.0/16
```

range.

This indicated that the VM did not have a valid IP configuration.

The issue was resolved by configuring the Hyper-V Internal adapter and assigning the Windows 10 VM a static IP address.

---

### Network Separation

The physical server network and Hyper-V lab network were separated into different subnets.

```text
Physical Network:
192.168.10.0/24

Lab Network:
192.168.20.0/24
```

This prevented the two networks from conflicting and provided a cleaner lab architecture.

---

### DNS Troubleshooting

DNS resolution was tested from the Windows 10 client.

Although `nslookup` initially displayed a timeout and identified the DNS server as `Unknown`, the requested records were still successfully returned.

This demonstrated the importance of testing actual name resolution rather than relying only on the displayed DNS server name.

---

# 📚 AZ-800 Skills Practiced

This lab currently covers practical experience in:

* Windows Server 2022 administration
* Hyper-V virtualization
* IPv4 networking
* Static IP configuration
* Virtual networking
* Active Directory Domain Services
* Active Directory domains and forests
* Domain Controllers
* DNS
* Active Directory users
* Active Directory security groups
* Organizational Units
* Windows domain joining
* Group Policy
* Workstation security
* Group Policy troubleshooting
* Windows command-line administration
* PowerShell
* Infrastructure troubleshooting

---

# 🚧 Planned Labs

The environment will continue to expand as additional AZ-800 topics are completed.

### Active Directory & Security

* [x] Active Directory Domain Services
* [x] Domain Controller
* [x] DNS
* [x] Organizational Units
* [x] Users
* [x] Security Groups
* [x] Domain-joined workstation
* [x] Workstation security GPO
* [ ] Password Policy
* [ ] Account Lockout Policy
* [ ] Additional security policies
* [ ] Delegation of Administration

### Networking

* [x] IPv4 configuration
* [x] Hyper-V Internal Network
* [x] DNS configuration
* [ ] DHCP Server
* [ ] DHCP scopes
* [ ] DHCP reservations
* [ ] DNS troubleshooting
* [ ] Windows Server routing concepts

### File Services

* [ ] File Server
* [ ] NTFS permissions
* [ ] Share permissions
* [ ] SMB file shares
* [ ] Access-based enumeration
* [ ] File Server Resource Manager

### Windows Server Administration

* [ ] PowerShell administration
* [ ] Remote Server Administration
* [ ] Windows Admin Center
* [ ] Server security
* [ ] Windows services
* [ ] Event Viewer
* [ ] Performance monitoring
* [ ] Backup and recovery

### Hybrid Administration

* [ ] Microsoft Entra ID integration concepts
* [ ] Azure management concepts
* [ ] Hybrid identity
* [ ] Azure Arc concepts
* [ ] Hybrid Windows Server management

---

# 📸 Screenshots

Screenshots and supporting documentation will be added to this repository as the lab progresses.

Screenshots will focus on:

* Hyper-V configuration
* Network configuration
* Active Directory
* DNS
* Group Policy
* Windows Server administration
* Troubleshooting
* Verification results

Sensitive information such as passwords, product keys, credentials, or confidential company information will not be published.

---

# 📈 Project Status

**Current Status: 🟢 Active Development**

Completed:

```text
Hyper-V                  ✅
Windows Server 2022      ✅
Windows 10 VM            ✅
Virtual Networking       ✅
Static IP Configuration  ✅
Active Directory         ✅
DNS                      ✅
Organizational Units     ✅
Users                    ✅
Security Groups          ✅
Domain Join              ✅
Group Policy             ✅
```

Next:

```text
Password & Account Lockout Policy
```

---

# 🎓 Purpose

This project is part of my practical development toward Windows Server administration and the Microsoft AZ-800 certification.

The goal is not only to study theory, but to build and troubleshoot a working Windows Server environment and document the process as a practical IT portfolio.

---

## Author

**Simphiwe Ngindi**

IT Support Technician | Aspiring Systems Administrator

GitHub: [@SimsNgindi](https://github.com/SimsNgindi)

```

### One small correction before you paste it

Because the repository is public, I would **remove the GitHub link at the bottom if your GitHub username is different from `SimsNgindi`**. Otherwise, the rest is ready to paste.

After you save it, your repository will already look substantially more like a **real Systems Administrator portfolio project** rather than just a GitHub notes page.
```
