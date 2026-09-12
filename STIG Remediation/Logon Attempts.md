# Account Logon Attempt Maximum
**STIG IDs**:  
- **WN10-AC-000010** - The number of allowed bad logon attempts must be configured to three or less 
---

## 1. Problem Statement / Vulnerability

### Info
- The account lockout feature, when enabled, prevents brute-force password attacks on the system.
- The higher this value is, the less effective the account lockout feature will be in protecting the local system.
- The number of bad logon attempts must be reasonably small to minimize the possibility of a successful password attack, while allowing for honest errors made during a normal user logon



---

## 2. Before Remediation (Initial State)


<img width="834" height="328" alt="Screenshot 2026-09-08 162609" src="https://github.com/user-attachments/assets/9af8be5a-7e25-4849-9596-4c4287a1beb3" />

<img width="904" height="312" alt="Screenshot 2026-09-08 161425" src="https://github.com/user-attachments/assets/d9d68941-89ac-451a-8612-edbf86055266" />



---

## 3. Manual Remediation (Local Security Policy)

- Open the Local Group Policy Editor >> Computer Configuration >> Windows Settings >> Security Settings >> Account
Policies >> Account Lockout Policy >> 'Account lockout threshold' to '3' or less invalid logon attempts (excluding
'0' which is unacceptable).

#Screenshots

<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/29d6f839-19aa-4536-9fbc-f734f295eb4e" />
<img width="747" height="279" alt="image" src="https://github.com/user-attachments/assets/0d93fa68-155c-480f-9e05-3acee2e61af9" />
<img width="748" height="268" alt="image" src="https://github.com/user-attachments/assets/d7685210-9f0e-4890-9201-04fa9ff1096d" />
<img width="747" height="289" alt="image" src="https://github.com/user-attachments/assets/2ac12aef-ef1f-4862-9af2-9df066d2cf63" />


<img width="746" height="292" alt="image" src="https://github.com/user-attachments/assets/4a6b271b-c17f-4009-844a-f87416ff4722" />

<img width="747" height="269" alt="image" src="https://github.com/user-attachments/assets/bde8c349-c789-456f-8f64-cdac48e7c8dc" />

<img width="744" height="455" alt="image" src="https://github.com/user-attachments/assets/434d704b-18bb-4c27-9b5c-e0a389400505" />

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


