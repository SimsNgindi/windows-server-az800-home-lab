# Active Directory OUs, Users and Groups

## Objective

Create a basic Active Directory organizational structure and configure users and security groups within the `lab.local` domain.

The objective is to practice centralized identity management and create an organized structure that can later be used for Group Policy and delegated administration.

---

## Organizational Units

The following Organizational Units (OUs) were created:

```text
lab.local
│
├── Users-Lab
├── Workstations
├── Servers
├── IT
└── Test
```

### OU Purpose

| OU           | Purpose                            |
| ------------ | ---------------------------------- |
| Users-Lab    | Lab user accounts                  |
| Workstations | Domain-joined client computers     |
| Servers      | Server computer accounts           |
| IT           | IT-related accounts and objects    |
| Test         | Testing objects and configurations |

---

## Workstation OU

The Windows 10 client computer account was moved into:

```text
Workstations
```

The computer account is:

```text
LAB-WIN10
```

This allows workstation-specific Group Policy settings to be applied to the computer.

---

## Creating a Domain User

A normal domain user account was created:

```text
Username: simphiwe.ngindi
First Name: Simphiwe
Last Name: Ngindi
```

The account is used to test normal domain authentication and Active Directory permissions.

---

## Domain Login

The Windows 10 client was successfully accessed using the domain account:

```text
LAB\simphiwe.ngindi
```

This confirmed that the Windows 10 computer was successfully communicating with the Active Directory domain.

---

## Security Group

A security group was created for IT administration:

```text
IT-Admins
```

Group configuration:

```text
Group Scope: Global
Group Type: Security
```

The domain user was added to the group:

```text
LAB\simphiwe.ngindi
```

---

## Verifying Group Membership

Group membership was verified from the Windows 10 client using:

```cmd
whoami /groups
```

The output confirmed membership in:

```text
LAB\IT-Admins
```

This verified that the user's Active Directory group membership was being applied correctly.

---

## Why OUs Are Important

Organizational Units provide a logical structure for managing Active Directory objects.

OUs can be used to:

* Organize users and computers
* Apply Group Policy
* Delegate administration
* Separate different types of objects
* Simplify Active Directory management

For example, the `Workstations` OU is used to contain domain-joined workstation computer accounts.

---

## Why Security Groups Are Important

Security groups allow permissions and access to be assigned to groups of users rather than individual users.

For example:

```text
IT-Admins
     |
     └── simphiwe.ngindi
```

Permissions can later be assigned to the `IT-Admins` group rather than configuring each administrator individually.

---

## Verification

The Active Directory configuration was verified by:

* Confirming the required OUs existed
* Moving `LAB-WIN10` into the `Workstations` OU
* Creating the `simphiwe.ngindi` domain account
* Creating the `IT-Admins` security group
* Adding the user to the security group
* Logging into Windows using the domain account
* Running `whoami /groups`
* Confirming `LAB\IT-Admins` membership

---

## Skills Practiced

This lab provided practical experience with:

* Active Directory Users and Computers
* Organizational Units
* Computer accounts
* User accounts
* Security groups
* Global security groups
* Domain authentication
* Group membership
* Active Directory organization
* Identity management

---

## Status

**Completed**
