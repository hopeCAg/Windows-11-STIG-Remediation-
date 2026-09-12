# Password Character Minimum
**STIG IDs**:  
- **WN11-AC-000035** - Passwords must, at a minimum, be 14 characters
---

## 1. Problem Statement / Vulnerability

### Info
- Information systems not protected with strong password schemes (including passwords of minimum length) provide the opportunity for anyone to crack the password, thus gaining access to the system and
compromising the device, information, or the local network


---

## 2. Before Remediation (Initial State)


<img width="730" height="341" alt="image" src="https://github.com/user-attachments/assets/5d2ba6cd-456a-4437-97c1-cb258fae2efe" />







---

## 3. Manual Remediation (Local Security Policy)

- Open the Local Group Policy Editor >> Computer Configuration >> Windows Settings >> Security Settings >> Account
Policies >>  Password Policy >> 'Minimum password length' to '14' characters


#Screenshots

<img width="745" height="327" alt="image" src="https://github.com/user-attachments/assets/c6118b13-1100-4450-9f71-cb0fbc9b779d" />

<img width="747" height="279" alt="image" src="https://github.com/user-attachments/assets/77b3dd52-2c2e-483e-bce8-51cbd20a7e2c" />

<img width="748" height="268" alt="image" src="https://github.com/user-attachments/assets/bea05544-5805-4bb0-856d-bccfb8c06565" />

<img width="747" height="289" alt="image" src="https://github.com/user-attachments/assets/adab7284-70c3-41b7-99c4-d6c65547fffc" />

<img width="747" height="210" alt="image" src="https://github.com/user-attachments/assets/e38f3f71-d927-4764-b9c7-7639cbfa3f8a" />

<img width="748" height="301" alt="image" src="https://github.com/user-attachments/assets/4cf1a4d9-d173-44f9-9cdb-6ff47bb18739" />

<img width="746" height="346" alt="image" src="https://github.com/user-attachments/assets/8f5e8836-f3fe-446e-a54d-ee61b5e6b266" />










---

## 4. Automated Remediation (PowerShell Script)



```powershell
net accounts /minpwlen:14
```

<img width="759" height="214" alt="image" src="https://github.com/user-attachments/assets/9d6a7ca5-f860-4959-b428-8c8954ee0834" />



## 5. Testing / Verification

 **Nessus / STIG Scan Pass**
   


---

