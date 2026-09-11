# RDS Password Prompt
**STIG IDs**:  
- **WN11-CC-000280** - Remote Desktop Services must always prompt a client for passwords upon connection.
---

## 1. Problem Statement / Vulnerability

### Info
- This setting controls the ability of users to supply passwords automatically as part of their remote desktop connection.
- Disabling this setting would allow anyone to use the stored credentials in a connection item to connect to the terminal server.


---

## 2. Before Remediation (Initial State)


<img width="789" height="291" alt="image" src="https://github.com/user-attachments/assets/1fbe07ad-53e6-4c71-8d7e-800e90e7a644" />







---

## 3. Manual Remediation 

- Open the Local Group Policy Editor >> Computer Configuration >>  Administrative Templates >> Windows Components >> Remote Desktop Services >> Remote Desktop Session Host >> Security >> 'Always prompt for password
upon connection' to 'Enabled'.rs


#Screenshots

<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/c6118b13-1100-4450-9f71-cb0fbc9b779d" />

<img width="745" height="289" alt="image" src="https://github.com/user-attachments/assets/f438cfd3-dedb-41dd-b23c-afca2d6e57ce" />

<img width="745" height="332" alt="image" src="https://github.com/user-attachments/assets/baae9b1e-3da2-4520-8d6a-22ee77788d81" />

<img width="745" height="339" alt="image" src="https://github.com/user-attachments/assets/4267e611-0554-40d3-aa5f-9d2495e2315c" />

<img width="745" height="283" alt="image" src="https://github.com/user-attachments/assets/2bf76ce7-829d-48e4-9d6b-4b5e99130428" />

<img width="745" height="352" alt="image" src="https://github.com/user-attachments/assets/203711a7-2cc5-4b61-ba12-995c22a09404" />

<img width="745" height="338" alt="image" src="https://github.com/user-attachments/assets/94ecb2e4-d2e9-4bdb-9046-f7ea9cb36dc0" />

<img width="745" height="303" alt="image" src="https://github.com/user-attachments/assets/0541d253-5fae-47da-96ac-32bb34cbafd8" />














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
