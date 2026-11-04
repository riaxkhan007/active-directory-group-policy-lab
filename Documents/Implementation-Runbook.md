# Implementation Runbook

This runbook records the build sequence used in the `corp.lab` lab. The instructions are written for a clean, isolated Windows Server 2022 environment. Re-check IP addressing and DNS in the live VM because the lab's virtual network changed during troubleshooting.

## 1. Prepare the domain controller

1. Install Windows Server 2022 and set a stable computer name (`DC01`).
2. Assign a static IPv4 address that is outside the VMware DHCP pool or create a DHCP reservation.
3. Set the preferred DNS server on the domain controller NIC to the domain controller's own IPv4 address after DNS is installed.
4. Install the Active Directory Domain Services and DNS Server roles.
5. Promote the server to a new forest named `corp.lab`.
6. Confirm the domain is available in Active Directory Users and Computers and DNS Manager.

## 2. Create OUs, users, and groups

Create these OUs under `corp.lab`:

- Management
- IT
- HR
- Finance
- Workstations

Create these security groups:

- `Management-Users`
- `IT-Admins`
- `HR-Users`
- `Finance-Users`

Create or place the representative user accounts in their matching OUs:

| User | OU | Group |
|---|---|---|
| `ahmad.khan` | Management | `Management-Users` |
| `ali.raza` | IT | `IT-Admins` |
| `sara.ahmed` | HR | `HR-Users` |
| `bilal.shah` | Finance | `Finance-Users` |

Check each user's Member Of tab and ensure the client computer account is placed in the Workstations OU.

## 3. Join the client

1. Set the client's preferred DNS server to the domain controller's IP address.
2. Confirm the client can resolve `DC01` and `corp.lab`.
3. Join `CLIENT01` to `corp.lab` using an authorized domain account.
4. Restart and sign in with a domain user such as `CORP\sara.ahmed`.

## 4. Create the shared folder

Local root:

`C:\SHARED FOLDER\Corp Lab Data`

Share name:

`Corp Lab Data`

UNC root:

`\\DC01\Corp Lab Data`

Create these folders:

```text
Corp Lab Data
├── Finance
├── HR DATA
├── IT
└── Management
```

For the final permissions model:

- Keep `SYSTEM` and local/domain Administrators with Full Control.
- Remove broad `Everyone: Full Control` share access.
- Use a limited share-level permission for authenticated domain users, then enforce department isolation with NTFS permissions on each subfolder.
- Grant the matching department group Modify on its own folder only, unless the lab design intentionally requires a different level.
- Review inheritance at the child folders and confirm one department cannot open another department's folder.

## 5. Configure domain account policies

Open Group Policy Management and edit the Default Domain Policy:

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies`

Configure Password Policy and Account Lockout Policy. The supplied screenshot records these current values: 24 remembered passwords, 50-day maximum age, 1-day minimum age, 5-character minimum length, complexity enabled, reversible encryption disabled, and lockout after 10 invalid attempts for 5 minutes with a 5-minute reset counter.

Before calling this a hardened baseline, raise the minimum password length and review lockout thresholds. See the Security Review document.

## 6. Configure department drive maps

For each department OU, create or edit a linked GPO and navigate to:

`User Configuration > Preferences > Windows Settings > Drive Maps`

Create a Mapped Drive preference with Action `Update`, the UNC folder path, the assigned drive letter, a clear label, and Reconnect enabled.

| Department | Location | Drive | Label |
|---|---|---|---|
| HR | `\\DC01\Corp Lab Data\HR DATA` | H: | HR Shared Drive |
| Finance | `\\DC01\Corp Lab Data\Finance` | F: | Finance Shared Drive |
| IT | `\\DC01\Corp Lab Data\IT` | I: | IT Shared Drive |
| Management | `\\DC01\Corp Lab Data\Management` | M: | Management Shared Drive |

Ensure each user object is in the corresponding OU. Group membership alone does not cause a GPO linked to an OU to apply unless security filtering or item-level targeting is configured.

## 7. Configure workstation restrictions

The lab contains a domain-root linked GPO named `GPO-Domain-Workstation-Security` and an HR-linked GPO named `GPO-HR-Desktop-Restrictions`.

The captured/working-session settings include removable-storage blocking, CD/DVD read/write blocking, AutoPlay disabled for all drives, Command Prompt restriction, Registry Editor restriction, Control Panel/Settings restriction, Settings Page Visibility, a legacy Internet Explorer proxy-setting restriction, specified-application restrictions for PowerShell executables, and removal of the Run command from Start.

**Critical correction:** inspect `Always install with elevated privileges`. The supplied screenshot shows it Enabled. Set it to Disabled in both User Configuration and Computer Configuration. Do not use AlwaysInstallElevated as a way to stop software installations. For a standard-user MSI restriction, configure the separate `Disable Windows Installer` policy as required by the lab and verify the effect.

## 8. Validation sequence

Use standard domain test accounts, not Domain Admin accounts:

1. Sign in as `CORP\sara.ahmed` on `CLIENT01`.
2. Confirm H: maps to `\\DC01\Corp Lab Data\HR DATA` and opens.
3. Confirm Control Panel is restricted.
4. Open Windows Settings separately and record its result.
5. Test removable USB storage with a non-sensitive test USB device.
6. Test CD/DVD access if a virtual or physical CD/DVD device exists.
7. Test Command Prompt, Registry Editor, PowerShell, and the Run command individually.
8. Repeat drive-map tests for Finance, IT, and Management users.
9. Review the applied GPOs with Group Policy Results or `gpresult` after the GUI-first tests.
10. Capture screenshots only after each outcome is clear.

## 9. Evidence handling

Use the numbered screenshots in `screenshots/` as source evidence. Capture fresh screenshots after any remediation. Redact any password, personal information, real organization information, or sensitive network detail before publishing.
