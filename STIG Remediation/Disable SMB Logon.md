# Password Character Minimum
**STIG IDs**:  
- **WN11-CC-000040** -  Insecure logons to an SMB server must be disabled
---

## 1. Problem Statement / Vulnerability

### Info
- Insecure guest logons allow unauthenticated access to shared folders.
- Shared resources on a system must require authentication to establish proper access

---

## 2. Before Remediation (Initial State)


<img width="679" height="250" alt="image" src="https://github.com/user-attachments/assets/bc87c19d-3796-4cbe-996d-7ced736e6ae2" />







---

## 3. Manual Remediation 

- Open the Local Group Policy Editor >> Computer Configuration >>  Administrative Templates >> Network >> Lanman Workstation >> 'Enable insecure guest logons' to 'Disabled'



### Screenshots:



<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/c6118b13-1100-4450-9f71-cb0fbc9b779d" />

<img width="745" height="268" alt="image" src="https://github.com/user-attachments/assets/3543af12-f0c5-401f-ae6d-acf600c5d391" />

<img width="745" height="289" alt="image" src="https://github.com/user-attachments/assets/5e740422-dfa3-45fa-8902-89a4d9f7edb7" />

<img width="745" height="349" alt="image" src="https://github.com/user-attachments/assets/9572addf-2e3a-47a7-9d60-b3dd49bb5a10" />

<img width="745" height="375" alt="image" src="https://github.com/user-attachments/assets/21ade819-2437-4006-9382-e00ea1ab5ab8" />


<img width="700" height="319" alt="image" src="https://github.com/user-attachments/assets/d1944fee-17e9-4f8a-a5c3-b8c075eaa6ab" />





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
