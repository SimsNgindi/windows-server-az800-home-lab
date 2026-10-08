# Network Configuration

## Objective

Configure a separate network for the Windows Server 2022 home lab and the Windows 10 virtual machine running on Hyper-V.

The objective was to create a reliable internal network that allows the domain controller and Windows client to communicate.

---

## Lab Network Design

The lab uses a separate subnet from the physical network.

### Physical Network

```text
Network: 192.168.10.0/24
Server: 192.168.10.1
```

### Hyper-V Lab Network

```text
Network: 192.168.20.0/24
Server: 192.168.20.1
Windows 10 VM: 192.168.20.10
```

The Hyper-V network uses an Internal virtual switch named:

```text
LAB-INTERNAL
```

---

## Server Network Configuration

The Windows Server 2022 host has two network interfaces:

| Interface                |   IP Address | Prefix |
| ------------------------ | -----------: | -----: |
| Ethernet                 | 192.168.10.1 |    /24 |
| vEthernet (Lab-Internal) | 192.168.20.1 |    /24 |

The two networks were intentionally placed on different subnets.

---

## Windows 10 Client Configuration

The Windows 10 VM was configured with:

```text
IP Address:      192.168.20.10
Subnet Mask:     255.255.255.0
Default Gateway: None
DNS Server:      192.168.20.1
```

The client uses the domain controller as its DNS server.

---

## Initial Problem

During the initial Hyper-V configuration, the Windows 10 VM received an APIPA address:

```text
169.254.x.x
```

An APIPA address indicated that the VM did not have a valid IPv4 configuration.

The Hyper-V virtual adapter was subsequently configured with:

```text
192.168.20.1/24
```

The Windows 10 VM was then configured with:

```text
192.168.20.10/24
```

---

## Connectivity Testing

Connectivity between the Windows 10 VM and the Hyper-V lab network was tested using:

```cmd
ping 192.168.20.1
```

The test completed successfully with:

```text
0% packet loss
```

---

## Verification

The server's IPv4 configuration was verified using PowerShell:

```powershell
Get-NetIPAddress -AddressFamily IPv4 |
Select-Object InterfaceAlias,IPAddress,PrefixLength
```

Expected configuration:

```text
vEthernet (Lab-Internal)    192.168.20.1    24
Ethernet                    192.168.10.1    24
```

---

## Lessons Learned

This part of the lab demonstrated:

* IPv4 addressing
* Subnet separation
* Hyper-V virtual networking
* Internal virtual switches
* Static IP configuration
* APIPA troubleshooting
* Network connectivity testing
* PowerShell network verification

---

## Status

**Completed**
