# Validation Results

**Evidence basis:** the supplied `Active directory.pdf` reference (12 pages) plus the configuration details recorded in the working session. This is an evidence log, not a claim that every configured policy has passed a client-side test.

## Confirmed by supplied screenshots

| Item | Evidence | Status | Notes |
|---|---|---|---|
| `corp.lab` domain and AD structure | Screenshot 03 | Evidenced | Department OUs and four security groups are visible. |
| `Corp Lab Data` share | Screenshots 04-05 | Evidenced | Share name/UNC visible. Screenshot 05 shows broad Everyone share permissions; review required. |
| Domain password policy | Screenshot 06 | Evidenced | Values visible; minimum length is 5 characters. |
| Account lockout policy | Screenshot 07 | Evidenced | 10 attempts; 5-minute lockout and reset window; administrator lockout enabled. |
| Department drive-map GPO setup | Screenshots 07-08 | Evidenced | HR, IT, Finance, and Management mapping configuration is shown. |
| HR user logon | Screenshot 11 | Evidenced | `sara.ahmed` welcome/session screen visible. |
| HR H: drive mapping | Screenshot 11 | Evidenced | HR DATA network location mapped as H:. |
| Control Panel restriction message | Screenshot 12 | Evidenced | Windows Restrictions dialog shown. |
| CD/DVD access denied | Screenshot 12 | Evidenced | D: access denied message shown. |
| Removable storage policy | Screenshot 09 | Configured in policy editor | All Removable Storage classes: Deny all access is Enabled. Client USB test not shown. |
| AutoPlay policy | Screenshot 09 | Configured in policy editor | Turn off AutoPlay Enabled for all drives. |
| Command Prompt restriction | Screenshot 10 | Configured in policy editor | Enabled. Client-side test not shown. |
| Control Panel/PC Settings policy | Screenshot 10 | Configured in policy editor | Enabled. Control Panel restriction message appears in screenshot 12; Settings not separately tested. |
| Proxy change restriction | Screenshot 11 | Configured in policy editor | Legacy Internet Explorer administrative template. |
| Always install with elevated privileges | Screenshot 10 | **Remediation required** | Enabled in the captured policy editor; set Disabled in both user and computer policy areas. |

## Configured in the working session; separate client proof still required

- Registry Editor restriction.
- PowerShell executable launch restriction (`powershell.exe`, `powershell_ise.exe`, `pwsh.exe`).
- Run command removal.
- Settings Page Visibility for selected Settings pages.
- USB storage denial from a test user's client session.
- Finance F:, IT I:, and Management M: drive access and cross-department denial.

## Recommended final test log

| Test account | Expected result | Actual result | Evidence filename |
|---|---|---|---|
| `CORP\sara.ahmed` | H: maps and opens HR DATA | Confirmed in screenshot | `11-sara-ahmed-login-hr-drive-and-proxy-policy.png` |
| `CORP\sara.ahmed` | Control Panel is blocked | Restrictions message shown | `12-control-panel-and-cd-dvd-access-denied-tests.png` |
| `CORP\sara.ahmed` | CD/DVD read is denied | Access denied shown | `12-control-panel-and-cd-dvd-access-denied-tests.png` |
| `CORP\sara.ahmed` | USB storage access is denied | Not evidenced | Capture after testing |
| `CORP\sara.ahmed` | CMD / Registry / PowerShell / Run restrictions work | Not evidenced | Capture after testing |
| `CORP\bilal.shah` | F: maps and opens Finance | Not evidenced | Capture after testing |
| `CORP\ali.raza` | I: maps and opens IT | Not evidenced | Capture after testing |
| `CORP\ahmad.khan` | M: maps and opens Management | Not evidenced | Capture after testing |

## How to record new results

After sign-in, record the client hostname, user, test date, policy, expected behavior, actual behavior, and screenshot filename. Mark a test `Pass` only when the behavior has been observed. Use `Fail` when the setting is not applied or the behavior is wrong, and `Not tested` when the test was not performed.
