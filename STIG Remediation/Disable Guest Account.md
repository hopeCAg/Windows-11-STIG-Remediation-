# Disable Guest Account
**STIG IDs**:  
- **WN11-SO-000010 - The built-in guest account must be disabled.  
---

## 1. Problem Statement / Vulnerability

### Info
- A system faces an increased vulnerability threat if the built-in guest account is not disabled.
- This account is a known account that exists on all Windows systems and cannot be deleted.
- This account is initialized during the installation of the operating system with no password assigned.



---

## 2. Before Remediation (Initial State)

<img width="831" height="569" alt="image" src="https://github.com/user-attachments/assets/922b9450-bada-441b-895d-ec947e7d25d9" />    <img width="410" height="504" alt="Screenshot 2026-09-09 152017" src="https://github.com/user-attachments/assets/f6512d97-aa18-4d7a-ae9a-02545db3f051" />





---

## 3. Manual Remediation (Local Security Policy)

- Open the Local Group Policy Editor >> Computer Configuration >> Windows Settings >> Security Settings >> Local Policies >> Security Options >> 'Accounts: Guest account status' to 'Disabled'.

#Screenshots

<img width="748" height="524" alt="Screenshot 2026-09-09 161324" src="https://github.com/user-attachments/assets/072c09b7-b22f-4379-8092-9430ae660c25" />
<img width="747" height="292" alt="Screenshot 2026-09-09 161348" src="https://github.com/user-attachments/assets/d776818f-7b48-45ba-9c1b-6e3f67b5c030" />
<img width="746" height="337" alt="Screenshot 2026-09-09 161406" src="https://github.com/user-attachments/assets/dc241e8e-6543-4b4d-a228-ef1ebafc781b" />
<img width="748" height="282" alt="Screenshot 2026-09-09 161442" src="https://github.com/user-attachments/assets/08d0c6b6-2462-44c6-8933-579fd7ff0a2a" />
<img width="747" height="312" alt="image" src="https://github.com/user-attachments/assets/a3d60701-aa98-457e-9ff7-e5e176f094f0" />

<img width="746" height="383" alt="Screenshot 2026-09-09 161532" src="https://github.com/user-attachments/assets/3f7ef555-89a3-4f21-a408-da76de67842f" />












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

