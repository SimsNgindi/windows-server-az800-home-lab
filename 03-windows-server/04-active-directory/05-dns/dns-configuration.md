# DNS Configuration

## Objective

Configure and verify DNS services in the Windows Server 2022 Active Directory lab.

DNS is a critical component of Active Directory because domain clients use DNS to locate the Domain Controller and resolve names within the `lab.local` domain.

---

## DNS Environment

| Setting       | Configuration |
| ------------- | ------------- |
| DNS Server    | SRV-DC01      |
| DNS Server IP | 192.168.20.1  |
| Domain        | lab.local     |
| Client        | LAB-WIN10     |
| Client DNS    | 192.168.20.1  |

---

## DNS Installation

DNS was installed as part of the Active Directory Domain Services deployment.

The Domain Controller provides DNS services for the `lab.local` domain.

The DNS server is hosted on:

```text
SRV-DC01
```

---

## Client DNS Configuration

The Windows 10 client was configured to use the Domain Controller as its preferred DNS server.

```text
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
DNS Server: 192.168.20.1
```

The client does not use a public DNS server such as Google DNS or Cloudflare DNS because domain clients should use the internal Active Directory DNS server.

---

## DNS Records

The Active Directory DNS zone contains records for the lab domain.

The primary domain is:

```text
lab.local
```

The Domain Controller can be resolved using:

```text
SRV-DC01.lab.local
```

The DNS environment allows the Windows 10 client to locate and communicate with the Domain Controller.

---

## DNS Testing

DNS resolution was tested from the Windows 10 client using:

```cmd
nslookup lab.local
```

The query successfully returned the domain records.

The Domain Controller was also tested using:

```cmd
nslookup SRV-DC01.lab.local
```

The query successfully returned the Domain Controller address.

Example:

```text
Name: SRV-DC01.lab.local
Address: 192.168.10.1
```

---

## DNS Troubleshooting

During testing, `nslookup` initially displayed:

```text
DNS request timed out.
Server: Unknown
Address: 192.168.20.1
```

However, the requested DNS records were subsequently returned successfully.

This demonstrated that DNS resolution was working even though the DNS server name was displayed as `Unknown`.

The `Server: Unknown` result can occur when reverse DNS/PTR resolution for the DNS server itself is not configured.

The important verification was that the required forward DNS records could be resolved successfully.

---

## Connectivity Testing

The Windows 10 client was also able to resolve and communicate with the Domain Controller by hostname.

For example:

```cmd
ping SRV-DC01.lab.local
```

This confirmed that DNS name resolution and network connectivity were functioning together.

---

## Why DNS Is Important to Active Directory

Active Directory relies heavily on DNS.

Domain clients use DNS to locate services provided by Domain Controllers.

Without working DNS:

* Domain authentication can fail
* Domain joining can fail
* Group Policy processing can fail
* Clients may not locate Domain Controllers
* Active Directory services may become unreliable

For this reason, the lab uses the Domain Controller as the DNS server for the Windows client.

---

## Verification Commands

### Test DNS resolution

```cmd
nslookup lab.local
```

### Test Domain Controller resolution

```cmd
nslookup SRV-DC01.lab.local
```

### Test connectivity by hostname

```cmd
ping SRV-DC01.lab.local
```

---

## Skills Practiced

This lab provided practical experience with:

* Windows DNS Server
* Active Directory integrated DNS
* DNS zones
* DNS name resolution
* Forward DNS lookups
* Reverse DNS concepts
* `nslookup`
* DNS troubleshooting
* Domain Controller name resolution
* DNS and Active Directory integration

---

## Status

**Completed**
