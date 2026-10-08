# Hyper-V Configuration

## Objective

Install and configure Hyper-V on Windows Server 2022 to create a virtualized environment for the Windows Server and Windows client lab.

The goal was to create an isolated virtual networking environment that could be used for practicing Windows Server administration and AZ-800 concepts.

---

## Hyper-V Installation

Hyper-V was installed on the Windows Server 2022 host.

After installation, the Hyper-V management console was opened using:

```text
Hyper-V Manager
```

The Hyper-V host was then used to create and manage the Windows 10 virtual machine.

---

## Virtual Switch

An Internal Hyper-V virtual switch was created.

```text
Switch Name: LAB-INTERNAL
Switch Type: Internal
```

The internal switch provides network connectivity between the Hyper-V host and virtual machines connected to the switch.

---

## Windows 10 Virtual Machine

A Windows 10 virtual machine was created for the lab.

### VM Configuration

| Setting          | Configuration |
| ---------------- | ------------- |
| VM Name          | LAB-WIN10     |
| Generation       | Generation 2  |
| Memory           | 2 GB          |
| Processors       | 2 vCPU        |
| Virtual Disk     | 40 GB         |
| Network          | LAB-INTERNAL  |
| Operating System | Windows 10    |

---

## Network Configuration

The Windows 10 VM was connected to:

```text
LAB-INTERNAL
```

The VM was later configured with the following static IP configuration:

```text
IP Address:      192.168.20.10
Subnet Mask:     255.255.255.0
Default Gateway: None
DNS Server:      192.168.20.1
```

The Hyper-V host's virtual Ethernet adapter was configured with:

```text
192.168.20.1/24
```

---

## Troubleshooting

During the initial configuration, the Windows 10 VM received an APIPA address in the:

```text
169.254.0.0/16
```

range.

This indicated that the VM did not have a valid IPv4 configuration.

The issue was resolved by configuring the Hyper-V Internal network and assigning the required static IP addresses.

After the configuration was corrected, the Windows 10 VM was able to communicate with the Hyper-V host on the lab network.

---

## Verification

Network connectivity was tested from the Windows 10 VM using:

```cmd
ping 192.168.20.1
```

The test was successful with:

```text
0% packet loss
```

The Windows 10 VM was therefore successfully connected to the Hyper-V Internal network.

---

## Skills Practiced

This lab provided practical experience with:

* Hyper-V installation
* Hyper-V Manager
* Virtual machine creation
* Generation 2 virtual machines
* Virtual CPU and memory allocation
* Virtual hard disks
* Hyper-V virtual switches
* Internal virtual networking
* Static IP configuration
* APIPA troubleshooting
* Virtual machine network troubleshooting

---

## Status

**Completed**
