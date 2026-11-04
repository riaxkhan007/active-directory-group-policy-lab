# Portfolio item copy

## Title
Active Directory & Group Policy Lab

## Role
Windows Server / Active Directory Administrator

## Short project description
Built a Windows Server 2022 Active Directory lab with departmental OUs and groups, SMB shared folders, mapped drives, domain account policies, and workstation restrictions. Captured HR login, H: drive, Control Panel, and CD/DVD validation evidence.

## Full description
Built a self-directed Windows Server 2022 lab for the corp.lab domain. Configured AD DS and DNS, departmental OUs and groups, SMB shared folders, four mapped drives, domain password and lockout policies, and Group Policy workstation restrictions. Evidence includes an HR domain logon, H: drive mapping, a Control Panel restriction message, and CD/DVD access denial. Includes an architecture diagram, implementation report, runbook, screenshots, and a security remediation review. Personal lab, not a client deployment; some controls still need client-side validation.

## Skills to select
- Active Directory
- Windows Server
- Group Policy
- DNS
- Network Administration

## Suggested media order
1. `assets/portfolio-cover.png` - cover image.
2. `docs/Technical-Implementation-Report.pdf` - technical report.
3. `assets/architecture.png` - logical architecture.
4. `screenshots/03-active-directory-ou-and-security-groups.png` - AD structure.
5. `screenshots/08-department-drive-mapping-gpos.png` - drive mappings.
6. `screenshots/11-sara-ahmed-login-hr-drive-and-proxy-policy.png` - HR session and H: drive.
7. `screenshots/12-control-panel-and-cd-dvd-access-denied-tests.png` - client validation evidence.

## Before publishing
- Use the **Full description** above in the Upwork description field (it is within the current 600-character limit). Keep the short description as an alternate teaser if the interface offers a separate summary field.
- Correct `Always install with elevated privileges` to Disabled in both User and Computer Configuration.
- Consider raising the minimum password length from 5 to at least 12/14 characters.
- Replace `Everyone: Full Control` share permissions with a narrower authenticated access model and verify NTFS restrictions.
- Ensure every line in the description matches the final evidence and use only screenshots that contain no credentials or sensitive information.
- Do not add a related Upwork job because this was a self-directed lab, not a client contract.
