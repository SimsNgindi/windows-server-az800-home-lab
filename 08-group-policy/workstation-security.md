# Group Policy – Workstation Security

## Objective

Configure and verify a Group Policy Object (GPO) for Windows workstation security and confirm that the policy is successfully applied to domain-joined computers.

## Lab Environment

* Domain: `lab.local`
* Domain Controller: `SRV-DC01`
* Client: `LAB-WIN10`
* Workstation OU: `Workstations`
* GPO: `LAB - Workstation Security`

## GPO Configuration

A new Group Policy Object named:

`LAB - Workstation Security`

was created and linked to the `Workstations` OU.

The following security setting was configured:

**Path:**

`Computer Configuration → Policies → Windows Settings → Security Settings → Local Policies → Security Options`

**Setting:**

`Interactive logon: Do not display last signed-in`

**Configuration:**

`Enabled`

This configuration prevents Windows from displaying the previous user's account name on the sign-in screen.

## Applying the Policy

The policy was manually refreshed on the Windows 10 client using:

```powershell
gpupdate /force
```

The command completed successfully.

## Verifying the Applied GPO

The following command was used to verify which Group Policies were applied:

```powershell
gpresult /r
```

The applied computer policies included:

* `LAB - Workstation Security`
* `Default Domain Policy`

This confirmed that the workstation was receiving the newly created GPO from Active Directory.

## Verification

The following were confirmed:

* GPO created successfully
* GPO linked to the `Workstations` OU
* `LAB-WIN10` is located in the `Workstations` OU
* `gpupdate /force` completed successfully
* `LAB - Workstation Security` appeared in `gpresult /r`
* `Default Domain Policy` was also applied

## Skills Demonstrated

* Group Policy Management
* Creating and linking GPOs
* Organisational Unit targeting
* Windows security policy configuration
* Group Policy troubleshooting
* `gpupdate`
* `gpresult`
* Active Directory policy management

## Status

Completed.
