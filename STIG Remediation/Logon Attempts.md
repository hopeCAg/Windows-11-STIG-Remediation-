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
net accounts /lockoutthreshold:3
```
<img width="630" height="227" alt="image" src="https://github.com/user-attachments/assets/513492ea-1aa7-4bef-bb5c-87734f36fa8f" />




## 5. Testing / Verification


  
 **Nessus / STIG Scan Pass**
   
<img width="1233" height="271" alt="image" src="https://github.com/user-attachments/assets/5f0de2f0-6edf-4813-a263-a41fb01d1126" />



---


