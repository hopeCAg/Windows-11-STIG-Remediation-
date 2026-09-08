# Windows-11-STIG-Remediation

Welcome to my **Windows 10 STIG v3r2** remediation project! This repository documents how I systematically remediated STIG findings from an initial Tenable Nessus STIG scan on a Windows 10 Azure VM.

## Table of Contents

1. [Project Overview](#project-overview)
2. [High-Priority STIG Controls](#high-priority-stig-controls)
3. [Remediation Workflow](#remediation-workflow)
4. [Scripts Folder](#scripts-folder)
5. [Sub-Pages / Documentation](#sub-pages--documentation)
6. [Initial Nessus Scan Results](#initial-nessus-scan-results)

---

## Project Overview

- **Purpose**: Demonstrate the practical process of scanning a Windows 10 Azure VM with Nessus, identifying STIG findings, remediating them with PowerShell or manual configuration, and verifying the result.
- **Scope**: Focus on the DISA Windows 10 STIG v3r2 controls.

## Chosen STIG Controls



| STIG ID(s)                      | Summary                                                 | Remediation Summary                                                        |
|---------------------------------|---------------------------------------------------------|--------------------------------------------------------------|
| WN11-AC-000010  | The number of allowed bad logon attempts must be configured to three or less.         |  *[Logon Attempts](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG-Summaries/Logon%20attempts)*                                      |
| WN11-SO-000010                   | The built-in guest account must be disabled.                           | *[Disable guest account](./docs/STIG-DisablePS2.md)*                                       |
| WN11-CC-000391 | Internet Explorer must be disabled for Windows 11.  | *[Disable Internet explorer](./docs/STIG-AccountLockout.md)*                                    |
| WN11-AC-000035        | Passwords must, at a minimum, be 14 characters.      | *[Password Character Minimum](./docs/STIG-PasswordComplexityRemediation.md)*                                       |
| WN11-SO-000280 | Passwords for enabled local Administrator accounts must be changed at least every 60 days.               | *[Administrator Maximum Password Age](./docs/STIG-DisableAutoPlay.md)*                                       |
| WN11-SO-000070                  | The machine inactivity limit must be set to 15 minutes, locking the system with the screensaver.  | *[Machine Inactivity Limit](./docs/STIG-ConfigureDEP.md)*                                       |
| WN11-AC-000020                  |The password history must be configured to 24 passwords remembered.                           | *[Password History Minimum](./docs/STIG-DisableWDigest.md)*                                       |
| WN11-CC-000040                  | Insecure logons to an SMB server must be disabled.                          | *[Disable SMB Logon](./docs/STIG-DisableSecondaryLogon.md)*                |
| WN11-CC-000280                  | Remote Desktop Services must always prompt a client for passwords upon connection.                          | *[RDS Password Prompt](./docs/STIG-DisableSecondaryLogon.md)*                |



## Scripts Folder

All PowerShell scripts are stored under [`scripts/`](./scripts). Each script references the relevant STIG ID(s) and includes usage instructions:

1. **[Set-STIG-EventLogSizes-GPO.ps1](./scripts/Set-STIG-EventLogSizes-GPO.ps1)**  
   - Automates **WN10-AU-000500**, **-000505**, **-000510** to ensure event log sizes meet STIG thresholds.

2. **[Disable-PowerShell2.ps1](./scripts/Disable-PowerShell2.ps1)**  
   - Remediates **WN10-00-000155** by removing the legacy PowerShell 2.0 feature, preventing downgrade attacks and enabling advanced logging in modern PowerShell versions.

3. **[Disable-WDigest.ps1](./scripts/Disable-WDigest.ps1)**  
   - Addresses **WN10-CC-000038** by setting `UseLogonCredential=0` to prevent plaintext password storage in LSASS for WDigest authentication.

4. **[Disable-AutoPlay.ps1](./scripts/Disable-AutoPlay.ps1)**  
   - Remediates **WN10-CC-000180**, **-000185**, **-000190** by disabling AutoPlay/AutoRun for all drives and devices, preventing autorun commands from executing.

5. **[Set-STIG-AccountLockout.ps1](./scripts/Set-STIG-AccountLockout.ps1)**  
   - Enforces **WN10-AC-000005**, **-000010**, **-000015** by setting account lockout threshold (3 attempts), lockout duration (15 minutes), and reset counter (15 minutes).

6. **[Set-STIG-PasswordComplexity.ps1](./scripts/Set-STIG-PasswordComplexity.ps1)**  
   - Configures **WN10-AC-000035**, **-000040** to require passwords of ≥14 characters and enable password complexity rules.

7. **[Disable-SecondaryLogon.ps1](./scripts/Disable-SecondaryLogon.ps1)**  
   - Implements **WN10-00-000175** by stopping and disabling the Secondary Logon service (seclogon), preventing privilege escalation scenarios.

8. **[Set-DEP-OptOut.ps1](./scripts/Set-DEP-OptOut.ps1)**  
   - Fulfills **WN10-00-000145** by setting Data Execution Prevention (DEP) to OptOut (or higher) using `bcdedit`.


## Sub-Pages / Documentation

For detailed breakdowns of each STIG item, see the [`docs/`](./docs) folder. Each page includes:
- The problem statement/vulnerability,
- Manual vs. automated remediation steps,
- Testing/verification screenshots,
- Rollback instructions (if needed).

### Example Sub-Page

- [Event Log Sizes (WN10-AU-000500, -000505, -000510)](./docs/STIG-EventLogSizes.md)

## Initial Nessus Scan Results

Below is a snippet or screenshot of my baseline Nessus scan showing various failures:

![STIG_BASELINE](https://github.com/user-attachments/assets/097155d2-f215-487c-a239-03ee1bade8ef)

## Initial STIG Scan
For the original Nessus scan results (showing the baseline STIG failures), see:
[Baseline-STIG-Scan.pdf](./reports/Baseline-STIG-Scan.pdf)

---

## Final Results

After applying all STIG remediations, I re-ran my Nessus scan. Initially, there were **137** failed checks, and now there are **122**, resulting in **15** items resolved.

This screenshot shows the updated scan results:

![STIG-final-results](https://github.com/user-attachments/assets/354360a0-255b-48cc-997f-16cac2a6defb)
*Figure: Nessus scan indicating 122 remaining items.*

---

## Post-Remediation Testing

After each STIG remediation, it is important to perform basic operational checks:
- Verify event logs for errors or warnings.
- Test critical applications and workflows to ensure no disruptions.
- Monitor for any unexpected system behavior or compatibility issues.
- If a service or feature fails, consider temporarily rolling back that specific STIG setting or create an exception per organizational policy.

## Ongoing Vulnerability Management (Maintenance Mode)

With the major vulnerabilities addressed, I will continue scanning regularly, applying patches, and reviewing STIG updates. This approach ensures new risks are caught early and the environment remains secure over time.

---

*Thank you for visiting! I hope this project helps illustrate how to methodically address STIG findings.*
