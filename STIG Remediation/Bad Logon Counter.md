# Bad Logon Counter
**STIG IDs**:  
- **WN11-AC-000015** - The period of time before the bad logon counter is reset must be configured to 15 minutes.
---

## 1. Problem Statement / Vulnerability

### Info
- The account lockout feature, when enabled, prevents brute-force password attacks on the system.
- This parameter specifies the period of time that must pass after failed logon attempts before the counter is reset to 0.
- The smaller this value is, the less effective the account lockout feature will be in protecting the local system



---

## 2. Before Remediation (Initial State)

<img width="757" height="326" alt="image" src="https://github.com/user-attachments/assets/618e2500-4631-40ae-b5da-44c9be885c3a" />





---

## 3. Manual Remediation (Local Security Policy)

- Open the Local Group Policy Editor >> Computer Configuration >> Windows Settings >> Security Settings >> Account Policies >> Account Lockout Policy >> 'Reset account lockout counter after' to '15' minutes.

### Screenshots

<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/cf690933-8e54-4f3d-9eb8-a3c7dc541ff5" />

<img width="747" height="279" alt="image" src="https://github.com/user-attachments/assets/bec6a143-f00a-4fba-a3cb-8d1f81ea617a" />
<img width="748" height="268" alt="image" src="https://github.com/user-attachments/assets/5448b298-2844-4739-aa78-2e9dd9fb8408" />

<img width="744" height="298" alt="image" src="https://github.com/user-attachments/assets/ab8aef4f-64a8-44c5-b47c-9db2703ce45c" />
<img width="740" height="281" alt="image" src="https://github.com/user-attachments/assets/79ad1131-1af6-454d-88fc-fa06f5ce792e" />

<img width="740" height="257" alt="image" src="https://github.com/user-attachments/assets/31f2a8af-50aa-4d51-b58d-e60627fe0f48" />


<img width="740" height="389" alt="image" src="https://github.com/user-attachments/assets/76cf4107-3d6e-49e6-b454-4247b01dd4d3" />






---

## 4. Automated Remediation (PowerShell Script)

<!-- See [`scripts/Set-STIG-AccountLockout.ps1`](../scripts/Set-STIG-AccountLockout.ps1). -->

```powershell
Write-Host "Configuring Account Lockout Policy (WN10-AC-000005, -000010, -000015)..." -ForegroundColor Cyan

try {
    # WN10-AC-000010: Allowed bad logon attempts ≤ 3
    net accounts /lockoutthreshold:3

    # WN10-AC-000005: Account lockout duration ≥ 15
    net accounts /lockoutduration:15

    # WN10-AC-000015: Reset lockout counter after ≥ 15
    net accounts /lockoutwindow:15

    Write-Host "Lockout policies configured successfully!"
}
catch {
    Write-Error "Failed to configure account lockout policies: $_"
}
```

<!-- **Reference**: [Official Microsoft net accounts documentation](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/net-commands-on-operating-systems).
-->
---

![AccountLockout_Script](https://github.com/user-attachments/assets/ec77f57b-a214-474e-ad72-55cc28f09b20)


## 5. Testing / Verification

<!--1. **Check Local Security Policy**  

   ![AccountLockout_After](https://github.com/user-attachments/assets/7923eb16-d87c-462f-b095-785bbaca65f0) -->
  
2. **Nessus / STIG Scan Pass**
   
   ![WN10-AC-000005](https://github.com/user-attachments/assets/8753e8e1-0a3e-48e7-a85e-1cc2741c1cff)

   ![WN10-AC-000010](https://github.com/user-attachments/assets/9cd27ac6-7d4e-47e7-9980-e4ee38b53ae8)

   ![WN10-AC-000015](https://github.com/user-attachments/assets/bbd9c8b3-3aee-4805-be20-6d505874a05c)


---
