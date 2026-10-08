# Domain Join and Authentication

## Objective

Join the Windows 10 client to the `lab.local` Active Directory domain and verify that domain authentication is working correctly.

This provides practical experience with domain membership, computer accounts, and domain user authentication.

---

## Environment

| Component         | Configuration |
| ----------------- | ------------- |
| Domain Controller | SRV-DC01      |
| Domain            | lab.local     |
| NetBIOS Domain    | LAB           |
| Client            | LAB-WIN10     |
| Client IP         | 192.168.20.10 |
| DNS Server        | 192.168.20.1  |

---

## Domain Join

The Windows 10 client was configured to use the Domain Controller as its DNS server:

```text
192.168.20.1
```

The client was then joined to the Active Directory domain:

```text
lab.local
```

The domain join created a computer account for the workstation in Active Directory.

The computer account is:

```text
LAB-WIN10
```

---

## Computer Account

After joining the domain, the `LAB-WIN10` computer account was located in Active Directory Users and Computers.

The computer account was moved into the:

```text
Workstations
```

Organizational Unit.

The resulting structure is:

```text
lab.local
└── Workstations
    └── LAB-WIN10
```

---

## Domain Authentication

A normal domain user was used to test authentication:

```text
LAB\simphiwe.ngindi
```

The user successfully logged into the Windows 10 client using the Active Directory account.

This confirmed that:

* The workstation was successfully joined to the domain
* The Domain Controller was reachable
* DNS resolution was functioning
* Active Directory authentication was working
* The domain user account was valid

---

## Verifying the Logged-In User

The logged-in domain account was verified using:

```cmd
whoami
```

The expected result was:

```text
LAB\simphiwe.ngindi
```

This confirmed that the Windows 10 client was authenticating against the Active Directory domain.

---

## Verifying Group Membership

The user's Active Directory group membership was checked using:

```cmd
whoami /groups
```

The output confirmed membership in:

```text
LAB\IT-Admins
```

This verified that the security group membership configured in Active Directory was being applied to the user's domain session.

---

## Domain Computer Groups

After joining the domain, the computer became a member of the domain computer security group.

The workstation was therefore managed as part of the Active Directory environment rather than as a standalone Windows computer.

---

## Troubleshooting

Successful domain joining depends on correct DNS configuration.

The Windows 10 client was configured to use:

```text
192.168.20.1
```

as its DNS server.

DNS was tested before and during the domain configuration using:

```cmd
nslookup lab.local
```

and:

```cmd
nslookup SRV-DC01.lab.local
```

The Domain Controller could also be reached using its hostname.

This helped confirm that the client could locate the Active Directory infrastructure.

---

## Verification Checklist

The following items were successfully verified:

* [x] Windows 10 client configured with a static IP
* [x] Client configured to use the Domain Controller for DNS
* [x] Client joined to `lab.local`
* [x] `LAB-WIN10` computer account created
* [x] Computer account moved to `Workstations`
* [x] Domain user created
* [x] Domain user successfully logged in
* [x] `whoami` confirmed domain authentication
* [x] `whoami /groups` confirmed `IT-Admins` membership

---

## Skills Practiced

This lab provided practical experience with:

* Windows domain joining
* Active Directory computer accounts
* Domain authentication
* DNS requirements for domain joining
* Domain user authentication
* Security group membership
* `whoami`
* `whoami /groups`
* Active Directory troubleshooting

---

## Status

**Completed**
