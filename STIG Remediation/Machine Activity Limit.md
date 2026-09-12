# Password Character Minimum
**STIG IDs**:  
- **WWN11-SO-000070** -  The machine inactivity limit must be set to 15 minutes, locking the system with
the screensaver
---

## 1. Problem Statement / Vulnerability

### Info
- Unattended systems are susceptible to unauthorized use and must be locked when unattended.
- The screen saver must be set at a maximum of 15 minutes and be password protected.
- This protects critical and sensitive data from exposure to unauthorized personnel with physical access to the computer. Satisfies: SRG-OS-000279-GPOS-00109, SRG-OS-000163-GPOS-00072


---

## 2. Before Remediation (Initial State)


<img width="739" height="266" alt="Screenshot 2026-09-11 014720" src="https://github.com/user-attachments/assets/9efaa092-d1c1-4b40-8b1c-0dfe8f94c839" />







---

## 3. Manual Remediation (Local Security Policy)

- Open the Local Group Policy Editor >> Computer Configuration >> Windows Settings >> Security Settings >>Local
Policies >> Security Options >> 'Interactive logon: Machine inactivity limit' to '900' seconds' or less, excluding '0'
which is effectively disabled

#Screenshots

<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/c6118b13-1100-4450-9f71-cb0fbc9b779d" />

<img width="747" height="279" alt="image" src="https://github.com/user-attachments/assets/77b3dd52-2c2e-483e-bce8-51cbd20a7e2c" />

<img width="748" height="268" alt="image" src="https://github.com/user-attachments/assets/bea05544-5805-4bb0-856d-bccfb8c06565" />

<img width="749" height="264" alt="Screenshot 2026-09-11 114117" src="https://github.com/user-attachments/assets/6efaae35-6796-4b53-a845-cb8a928d1fef" />

<img width="749" height="260" alt="Screenshot 2026-09-11 114225" src="https://github.com/user-attachments/assets/5a0acb02-e021-481b-8eb4-5c5dcd8992ca" />

<img width="750" height="272" alt="Screenshot 2026-09-11 114427" src="https://github.com/user-attachments/assets/33dc1ecc-1ed5-458f-b8a7-af629d42eb9a" />

<img width="742" height="419" alt="Screenshot 2026-09-11 114558" src="https://github.com/user-attachments/assets/7c0c2c3c-9a8f-432a-819c-b646cde6b62e" />










---

## 4. Automated Remediation (PowerShell Script)

<!-- See [`scripts/Set-STIG-AccountLockout.ps1`](../scripts/Set-STIG-AccountLockout.ps1). -->

```powershell
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name InactivityTimeoutSecs -Value 900 -Type DWord -Force
```

<img width="629" height="254" alt="image" src="https://github.com/user-attachments/assets/c8adf4ad-c9a1-4dbc-a5bc-29199b936139" />


---



## 5. Testing / Verification


**Nessus / STIG Scan Pass**
   

<img width="1230" height="255" alt="image" src="https://github.com/user-attachments/assets/787a1896-dc2c-4206-9620-e773517a1d7b" />


---
