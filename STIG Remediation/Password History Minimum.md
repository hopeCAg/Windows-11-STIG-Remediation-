# Password History Minimum
**STIG IDs**:  
- **WN11-AC-000020** - The password history must be configured to 24 passwords remembered.
---

## 1. Problem Statement / Vulnerability

### Info
- A system is more vulnerable to unauthorized access when system users recycle the same password several times without being required to change a password to a unique password on a regularly scheduled basis.
- This enables users to effectively negate the purpose of mandating periodic password changes.
- The default value is 24 for Windows domain systems.
- DOD has determined this is the appropriate value for all Windows systems

---

## 2. Before Remediation (Initial State)


<img width="1108" height="320" alt="image" src="https://github.com/user-attachments/assets/43eba2df-07ca-40d2-9211-475b1b920837" />







---

## 3. Manual Remediation

- Open the Local Group Policy Editor >> Computer Configuration >> Windows Settings >> Security Settings >> Account
Policies >>  Password Policy >>  'Enforce password history' to '24' passwords remembered. For Intune-managed systems: Revise the Intune policy to set password history policy to '24'
passwords remembered.


#Screenshots

<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/c6118b13-1100-4450-9f71-cb0fbc9b779d" />

<img width="747" height="279" alt="image" src="https://github.com/user-attachments/assets/77b3dd52-2c2e-483e-bce8-51cbd20a7e2c" />

<img width="748" height="268" alt="image" src="https://github.com/user-attachments/assets/bea05544-5805-4bb0-856d-bccfb8c06565" />

<img width="747" height="289" alt="image" src="https://github.com/user-attachments/assets/adab7284-70c3-41b7-99c4-d6c65547fffc" />

<img width="747" height="210" alt="image" src="https://github.com/user-attachments/assets/e38f3f71-d927-4764-b9c7-7639cbfa3f8a" />

<img width="750" height="314" alt="image" src="https://github.com/user-attachments/assets/ed11294c-03d3-4f4b-8e4f-88e69cfd33df" />

<img width="745" height="384" alt="image" src="https://github.com/user-attachments/assets/fbf85149-bd60-4d62-846a-be4423cf025f" />









---

## 4. Automated Remediation (PowerShell Script)



```powershell
net accounts /uniquepw:24
```

<img width="755" height="233" alt="image" src="https://github.com/user-attachments/assets/452085a0-de6d-4539-a16f-dc08e11bd5ea" />


## 5. Testing / Verification

  
 **Nessus / STIG Scan Pass**

<img width="1224" height="262" alt="image" src="https://github.com/user-attachments/assets/a85932db-aa76-466a-b5b4-f87cc2852b92" />


---
