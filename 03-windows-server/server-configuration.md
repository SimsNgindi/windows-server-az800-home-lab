# Windows Server 2022 Configuration

## Objective

Install and configure Windows Server 2022 as the main server for the AZ-800 home lab.

The server is used as the foundation for the lab environment and later provides Active Directory Domain Services and DNS services.

---

## Server Configuration

The Windows Server 2022 machine was configured with the following details:

| Setting          | Configuration        |
| ---------------- | -------------------- |
| Operating System | Windows Server 2022  |
| Server Name      | SRV-DC01             |
| Role             | Domain Controller    |
| Domain           | lab.local            |
| NetBIOS Domain   | LAB                  |
| RAM              | 8 GB                 |
| Virtualization   | Hyper-V              |
| DNS              | Active Directory DNS |

---

## Server Name

The server was renamed to:

```text
SRV-DC01
```

The naming convention identifies the machine as the primary server/domain controller for the lab.

---

## Network Interfaces

The server has two network connections.

### Physical Ethernet

```text
IP Address: 192.168.10.1
Subnet: /24
```

### Hyper-V Lab Network

```text
Interface: vEthernet (Lab-Internal)
IP Address: 192.168.20.1
Subnet: /24
```

The physical network and the Hyper-V lab network use separate subnets.

---

## IPv4 Verification

The server's IPv4 configuration was verified using PowerShell:

```powershell
Get-NetIPAddress -AddressFamily IPv4 |
Select-Object InterfaceAlias,IPAddress,PrefixLength
```

The expected configuration includes:

```text
vEthernet (Lab-Internal)    192.168.20.1    24
Ethernet                    192.168.10.1    24
```

---

## Server Roles

The Windows Server 2022 installation was later configured to provide infrastructure services for the lab.

The main role deployed is:

```text
Active Directory Domain Services
```

DNS was also installed as part of the Active Directory Domain Services deployment.

---

## Domain Controller

The server was promoted to a Domain Controller for the lab domain:

```text
Domain: lab.local
NetBIOS: LAB
Domain Controller: SRV-DC01
```

The Domain Controller provides authentication and directory services for the Windows 10 client.

---

## Server Management

The following Windows Server management tools are being used throughout the lab:

* Server Manager
* Hyper-V Manager
* Active Directory Users and Computers
* Group Policy Management
* DNS Manager
* PowerShell
* Command Prompt

---

## Troubleshooting

During the initial lab setup, network configuration issues were encountered between the physical network and the Hyper-V Internal network.

The lab network was separated onto:

```text
192.168.20.0/24
```

This provided a dedicated network for the virtual machines and avoided conflicts with the physical network.

---

## Verification

The Windows Server environment was verified by:

* Confirming the server hostname
* Confirming IPv4 configuration
* Confirming Hyper-V networking
* Confirming Active Directory installation
* Confirming DNS functionality
* Confirming communication with the Windows 10 client

---

## Skills Practiced

This lab provided practical experience with:

* Windows Server 2022
* Server naming and configuration
* IPv4 configuration
* PowerShell network administration
* Server Manager
* Hyper-V
* Server roles
* Active Directory Domain Services
* Domain Controller deployment
* DNS
* Infrastructure troubleshooting

---

## Status

**Completed**
