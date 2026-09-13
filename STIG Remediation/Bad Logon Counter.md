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

## 3. Manual Remediation 
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
net accounts /lockoutthreshold:5 /lockoutduration:15 /lockoutwindow:15
```

<img width="635" height="251" alt="image" src="https://github.com/user-attachments/assets/f31e7a5c-0fb6-4d91-bd03-153a99177c05" />




## 5. Testing / Verification

 **Nessus / STIG Scan Pass**
   
<img width="1229" height="259" alt="image" src="https://github.com/user-attachments/assets/19799883-b5c2-4a82-ae1f-329931992bd2" />


---
