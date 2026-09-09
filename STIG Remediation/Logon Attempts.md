# Account Logon Attempt Maximum
**STIG IDs**:  
- **WN10-AC-000010** (Number of allowed bad logon attempts ≤ 3)  
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

<img width="596" height="357" alt="image" src="https://github.com/user-attachments/assets/0609de2c-ea68-445e-a28a-44747a642bef" />


<img width="541" height="203" alt="image" src="https://github.com/user-attachments/assets/1fd08653-1de6-4666-b579-b071a1961059" />

<img width="541" height="257" alt="image" src="https://github.com/user-attachments/assets/c1b00f29-f21f-4002-bf87-a04afd78235b" />

<img width="541" height="259" alt="image" src="https://github.com/user-attachments/assets/df58d298-566e-41d6-a16c-2c6df86cdeef" />

<img width="541" height="250" alt="image" src="https://github.com/user-attachments/assets/f18fae22-bcf7-464c-93a6-72c2e59ceea0" />

<img width="541" height="257" alt="image" src="https://github.com/user-attachments/assets/30119ce1-68b0-4b04-bf61-af53a6a6b71f" />

<img width="606" height="404" alt="image" src="https://github.com/user-attachments/assets/3ccb198a-a6ad-45eb-8fa3-3a07ea256e69" />






---

## 4. Automated Remediation (PowerShell Script)

See [`scripts/Set-STIG-AccountLockout.ps1`](../scripts/Set-STIG-AccountLockout.ps1).

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

**Reference**: [Official Microsoft net accounts documentation](https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/net-commands-on-operating-systems).

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


---

## 7. Final Results

By setting **lockout** threshold, duration, and reset counter properly:

- **You** mitigate brute-force attacks on local accounts.  
- **WN10-AC-000005**, **-000010**, and **-000015** will pass in **DISA Windows 10 STIG v3r2**.  
