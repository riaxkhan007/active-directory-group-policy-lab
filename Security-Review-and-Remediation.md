# Security Review and Remediation

This review is based on the supplied 12-page evidence PDF and the lab configuration details recorded during the working session. It separates settings that are visible in evidence from recommendations for the next pass.

## Priority 1 - Correct before describing the lab as hardened

### 1. `Always install with elevated privileges` is Enabled in the evidence

The screenshot of the Windows Installer policy shows **Always install with elevated privileges = Enabled**. This setting is not a software-installation block. Windows Installer can run packages with elevated system privileges when the relevant policy is set in both user and computer policy areas. Microsoft advises avoiding this setting because a non-administrator may be able to install software with elevated privileges and access protected locations.

**Remediation:**

1. Open the central security GPO.
2. In `Computer Configuration > Policies > Administrative Templates > Windows Components > Windows Installer`, set **Always install with elevated privileges** to **Disabled**.
3. In `User Configuration > Policies > Administrative Templates > Windows Components > Windows Installer`, set the same policy to **Disabled**.
4. If the intended control is to prevent standard users from installing MSI packages, configure the distinct **Disable Windows Installer** policy to Enabled and select the appropriate option (for this lab, `Always` was the intended restriction).
5. Re-check the policy settings and test with a standard user.

Microsoft references:
- https://learn.microsoft.com/en-us/windows/desktop/Msi/windows-installer-best-practices
- https://learn.microsoft.com/en-us/windows/win32/msi/machine-policies

### 2. Password minimum length is 5 characters

The Default Domain Policy screenshot records a minimum password length of **5 characters**. Complexity is enabled, but a five-character minimum is weak for a modern lab baseline.

**Remediation:** raise the minimum length to at least 12 characters (14 is a stronger lab target), ensure test passwords comply, and capture the updated policy screen. Keep reversible encryption disabled.

### 3. Share-level permission grants Everyone Full Control

The share-permissions screenshot for `Corp Lab Data` shows `Everyone` with Full Control, Change, and Read allowed, alongside Administrators. Even when NTFS folder ACLs are restrictive, broad share permissions make the overall model harder to reason about and easier to misconfigure later.

**Remediation:** remove `Everyone` from the share ACL; add an appropriate authenticated domain principal with only the share-level access required (for example, Change/Read), retain Administrators Full Control, and enforce department isolation with NTFS permissions. Re-check the root and all four child folders.

## Priority 2 - Validate GPO scope and exclusions

### 4. Domain-root GPO scope is broad

`GPO-Domain-Workstation-Security` is described in the working notes as linked at the domain root. This can deliver Computer Configuration settings to domain computers beyond the intended client OU and User Configuration settings to users beyond the intended standard-user population. Domain controllers and administrator accounts may receive settings that were designed for ordinary workstations.

**Remediation:** separate workstation-computer controls from standard-user restrictions where practical. Link computer settings to the Workstations OU. Scope user restrictions to the intended department/user OUs or an explicitly maintained security group. Exclude administrative and service accounts from interactive user lockdown where appropriate. Review inheritance, security filtering, and loopback processing before changing scope.

### 5. Account lockout values need review

The supplied screenshot records 10 invalid attempts, a 5-minute lockout, a 5-minute reset counter, and Allow Administrator account lockout enabled. These are documented as-is, not endorsed as a universal security baseline.

**Remediation:** choose a deliberate lockout threshold and duration for the lab, document the trade-off between brute-force resistance and accidental lockout, and test that administrative recovery remains possible.

## Priority 3 - Complete the client verification matrix

The supplied screenshots show an HR login, H: drive, Control Panel restriction message, and CD/DVD access denial. The following controls appear in the working-session configuration but do not have clear client-side pass evidence in the supplied PDF:

- USB storage blocking
- Command Prompt blocking
- Registry Editor blocking
- PowerShell application restriction
- Run command removal
- Windows Settings access separately from Control Panel
- Finance, IT, and Management drive mappings

Test each item with a standard user, record Pass / Fail / Not tested, and retain a screenshot for each pass. Do not describe a configured policy as tested until its behavior has been observed on the client.

## Recommended final posture

- Restrict broad share permissions and validate the NTFS ACLs.
- Disable AlwaysInstallElevated in both policy branches.
- Raise the domain minimum password length.
- Re-scope the domain-root security GPO to workstation computers and standard users intentionally.
- Verify every department mapping and restriction with a non-administrator account.
- Record the date, test account, client, and result in the validation log.
