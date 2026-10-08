# Active Directory Domain Services Deployment

## Objective

Deploy Active Directory Domain Services (AD DS) on Windows Server 2022 and create a new Active Directory domain for the home lab.

The objective is to gain practical experience with Domain Controllers, Active Directory domains, authentication, and centralized administration.

---

## Active Directory Environment

The lab uses the following Active Directory configuration:

| Setting           | Configuration                   |
| ----------------- | ------------------------------- |
| Domain Controller | SRV-DC01                        |
| Domain            | lab.local                       |
| NetBIOS Domain    | LAB                             |
| Forest            | lab.local                       |
| Operating System  | Windows Server 2022             |
| DNS               | Active Directory Integrated DNS |

---

## AD DS Installation

The Active Directory Domain Services server role was installed on Windows Server 2022 using Server Manager.

The AD DS role provides centralized identity and authentication services for the Windows lab environment.

After installing the role, the server was promoted to a Domain Controller.

---

## Creating the Forest

A new Active Directory forest was created.

```text
Forest Root Domain:
lab.local
```

The domain uses:

```text
NetBIOS Name:
LAB
```

The resulting Active Directory structure is:

```text
Forest: lab.local
└── Domain: lab.local
    └── Domain Controller: SRV-DC01
```

---

## Domain Controller

The Windows Server 2022 server was promoted to a Domain Controller.

The Domain Controller is:

```text
SRV-DC01
```

It provides:

* Active Directory Domain Services
* Authentication
* Directory services
* DNS
* Domain management
* Group Policy infrastructure

---

## DNS Integration

DNS was installed as part of the Active Directory deployment.

The Windows 10 client uses the Domain Controller as its DNS server:

```text
DNS Server:
192.168.20.1
```

This allows domain clients to locate Active Directory services and resolve names within the `lab.local` domain.

---

## Domain Authentication

A Windows 10 client was successfully joined to the:

```text
lab.local
```

domain.

The client can authenticate using domain accounts in the following format:

```text
LAB\username
```

Example:

```text
LAB\simphiwe.ngindi
```

---

## Verification

Active Directory functionality was verified by:

* Confirming the `lab.local` domain
* Confirming `SRV-DC01` as the Domain Controller
* Confirming DNS functionality
* Joining the Windows 10 client to the domain
* Logging into the client using a domain account
* Verifying Active Directory group membership

---

## Troubleshooting

During the lab, DNS and network configuration were tested to ensure the Windows 10 client could communicate with the Domain Controller.

The client was configured to use:

```text
192.168.20.1
```

as its DNS server.

DNS resolution was tested using:

```cmd
nslookup lab.local
```

The Domain Controller hostname was also tested:

```cmd
nslookup SRV-DC01.lab.local
```

The client successfully resolved the domain and Domain Controller records.

---

## Skills Practiced

This lab provided practical experience with:

* Active Directory Domain Services
* Domain Controllers
* Active Directory forests
* Active Directory domains
* NetBIOS domain names
* Domain authentication
* DNS integration with Active Directory
* Windows domain joining
* Domain account authentication
* Active Directory troubleshooting

---

## Status

**Completed**
