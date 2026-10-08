# Password and Account Lockout Policy

## Objective

Configure and verify domain-level password and account lockout policies using Group Policy in the `lab.local` Active Directory environment.

## Lab Environment

* Domain: `lab.local`
* Domain Controller: `SRV-DC01`
* Client: `LAB-WIN10`
* Group Policy Object: `Default Domain Policy`

## Password Policy

The password policy was configured under:

`Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy`

The following settings were configured:

| Setting                                     |        Value |
| ------------------------------------------- | -----------: |
| Enforce password history                    |  5 passwords |
| Maximum password age                        |      90 days |
| Minimum password age                        |        1 day |
| Minimum password length                     | 8 characters |
| Password must meet complexity requirements  |      Enabled |
| Store passwords using reversible encryption |     Disabled |

## Account Lockout Policy

The account lockout policy was configured under:

`Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy`

The following settings were configured:

| Setting                             |              Value |
| ----------------------------------- | -----------------: |
| Account lockout threshold           | 5 invalid attempts |
| Account lockout duration            |         15 minutes |
| Reset account lockout counter after |         15 minutes |

## Applying the Policy

The policy was refreshed on the Windows 10 client using:

```cmd
gpupdate /force
```

The update completed successfully.

## Group Policy Verification

The following command was used to verify the applied computer policies:

```cmd
gpresult /scope computer /r
```

The following Group Policy Objects were confirmed:

* `Default Domain Policy`
* `LAB - Workstation Security`

## Effective Policy Verification

The effective account policy was verified using:

```cmd
net accounts
```

The output confirmed the configured password and account lockout settings on the Windows 10 client.

## Skills Demonstrated

* Active Directory domain policy management
* Password policy configuration
* Account lockout policy configuration
* Group Policy management
* Domain security configuration
* `gpupdate`
* `gpresult`
* `net accounts`
* Policy verification and troubleshooting

## Status

Completed.
