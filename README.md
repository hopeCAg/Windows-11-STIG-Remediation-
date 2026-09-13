# Windows-11-STIG-Remediation


## Overview

 This report documents the identification, remediation, and verification of a set of Windows 11 DISA STIG (Security Technical Implementation Guide) findings. STIGs are configuration security standards published by the Defense Information Systems Agency (DISA) to reduce the attack surface of DoD information systems; they are also widely adopted outside of DoD environments as a hardening baseline for Windows endpoints.










## Chosen STIG Controls



| STIG ID(s)                   | Severity   | Summary                                                 | Remediation Summary                                                        |
|---------------------------------|-----------|---------------------------------------------------------|--------------------------------------------------------------|
| WN11-AC-000010  | CAT I| The number of allowed bad logon attempts must be configured to three or less.         |  *[Logon Attempts](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Logon%20Attempts.md)*                                      |
| WN11-SO-000010    | CAT I               | The built-in guest account must be disabled.                           | *[Disable guest account](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Disable%20Guest%20Account.md)*                                       |
| WN11-AC-000015 | CAT III| The period of time before the bad logon counter is reset must be configured to 15 minutes.  | *[Bad logon Counter](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Bad%20Logon%20Counter.md)*                                    |
| WN11-AC-000035   | CAT II     | Passwords must, at a minimum, be 14 characters.      | *[Password Character Minimum](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Password%20Character%20Minimum.md)*                                       |
| WN11-AC-000030 | CAT III| The minimum password age must be configured to at least 1 day.               | *[Minimum Password Age](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Minimum%20Password%20Age.md)*                                       |
| WN11-SO-000070   | CAT II               | The machine inactivity limit must be set to 15 minutes, locking the system with the screensaver.  | *[Machine Inactivity Limit](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Machine%20Activity%20Limit.md)*                                       |
| WN11-AC-000020      | CAT II            |The password history must be configured to 24 passwords remembered.                           | *[Password History Minimum](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Password%20History%20Minimum.md)*                                       |
| WN11-CC-000040     | CAT I             | Insecure logons to an SMB server must be disabled.                          | *[Disable Insecure SMB Logon](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/Disable%20SMB%20Logon.md)*                |
| WN11-CC-000280    | CAT I              | Remote Desktop Services must always prompt a client for passwords upon connection.                          | *[RDS Password Prompt](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20Remediation/RDS%20Password%20Prompt.md)*                |





## Initial Scan Results



<img width="1220" height="391" alt="image" src="https://github.com/user-attachments/assets/d9803406-92a7-4899-9d1d-ea2f5143a2f4" />



See: [Initial-Stig-Scan](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20reports/Initial%20STIG%20Scan.pdf)

---

## Final Results

Scan results after the chosen STIG audit errors were remedied:
<img width="1224" height="419" alt="image" src="https://github.com/user-attachments/assets/6c2b7524-a12f-46ad-8657-fef8e7f74fe1" />



See: [Final-Stig-Scan](https://github.com/hopeCAg/Windows-11-STIG-Remediation-/blob/main/STIG%20reports/Final%20STIG%20Scan.pdf)


---



## Lessons Learned 
Registry-backed GPO settings often exist in two places: the runtime/service key (e.g. under CurrentControlSet\Services or \Control) and the Policies key (under SOFTWARE\Policies\Microsoft\...). Automated STIG scanners and the Local Group Policy Editor do not always read the same one. When a control fails to pass scan despite a registry value being correct, check both locations.
