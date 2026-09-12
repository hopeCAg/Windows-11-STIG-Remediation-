# Disable Insecure SMB logons
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
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation" -Name AllowInsecureGuestAuth -Value 0 -Type DWord
```

<img width="628" height="204" alt="image" src="https://github.com/user-attachments/assets/f89c7fe0-2ca2-4c70-80fc-e732892d4b60" />


## 5. Testing / Verification

<img width="1224" height="260" alt="image" src="https://github.com/user-attachments/assets/aefa7435-ce0f-4f7d-9ef2-0d008497b706" />

  
 **Nessus / STIG Scan Pass**
   


---
