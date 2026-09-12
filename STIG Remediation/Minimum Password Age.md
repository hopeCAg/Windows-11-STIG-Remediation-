# Minimum Password Age
**STIG IDs**:  
- **WN11-SO-000030** - The minimum password age must be configured to at least 1 day.
---

## 1. Problem Statement / Vulnerability

### Info
- Permitting passwords to be changed in immediate succession within the same day allows users to cycle passwords through their history database.
- This enables users to effectively negate the purpose of mandating periodic password changes.

---

## 2. Before Remediation (Initial State)


<img width="728" height="341" alt="image" src="https://github.com/user-attachments/assets/c26dd840-caf8-4dbc-a686-751d55fcfb7e" />







---

## 3. Manual Remediation (Local Security Policy)

- Open the Local Group Policy Editor >> Computer Configuration >> Windows Settings >> Security Settings >> Account
Policies >>  Password Policy >>  'Minimum Password Age' to at least '1' day.

#Screenshots

<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/c6118b13-1100-4450-9f71-cb0fbc9b779d" />

<img width="747" height="279" alt="image" src="https://github.com/user-attachments/assets/77b3dd52-2c2e-483e-bce8-51cbd20a7e2c" />

<img width="748" height="268" alt="image" src="https://github.com/user-attachments/assets/bea05544-5805-4bb0-856d-bccfb8c06565" />

<img width="747" height="289" alt="image" src="https://github.com/user-attachments/assets/adab7284-70c3-41b7-99c4-d6c65547fffc" />

<img width="747" height="210" alt="image" src="https://github.com/user-attachments/assets/e38f3f71-d927-4764-b9c7-7639cbfa3f8a" />

<img width="744" height="275" alt="image" src="https://github.com/user-attachments/assets/2acee3f6-dd86-4f16-a870-922ddedf201e" />



<img width="744" height="451" alt="image" src="https://github.com/user-attachments/assets/6d8a0de4-1737-44c5-a7f6-2bffeb0f833e" />










---

## 4. Automated Remediation (PowerShell Script)

<!-- See [`scripts/Set-STIG-AccountLockout.ps1`](../scripts/Set-STIG-AccountLockout.ps1). -->

```powershell
net accounts /minpwage:1
```

<img width="628" height="256" alt="image" src="https://github.com/user-attachments/assets/c12bfd35-cca3-4825-a87c-93c2efdaecfe" />



## 5. Testing / Verification

 **Nessus / STIG Scan Pass**
   



---

