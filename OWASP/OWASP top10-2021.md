# 🔑 Broken Access Control (BAC)

## 📌 What is Access Control?
Access control ensures **who** (user, role, identity) can perform **what** (action, resource access) in a system.  
- **Authentication** → Verifies identity (login).  
- **Authorization** → Determines allowed actions.  

**Broken Access Control (BAC)** = Failure to properly enforce authorization rules, letting attackers do things they shouldn’t.

---

## 🚨 Examples of Broken Access Control
1. **Insecure Direct Object References (IDOR)**  
   - Example:  
     ```
     https://bank.com/account?id=123   → your account
     https://bank.com/account?id=124   → another user’s account
     ```

2. **Privilege Escalation**  
   - Normal user becomes **admin** by changing a cookie/token.  

3. **Force Browsing**  
   - Accessing restricted pages by guessing URLs (`/admin`, `/deleteUser`).  

4. **Bypassing Access Controls**  
   - Directly calling API endpoints without proper role checks.  

5. **CORS Misconfigurations**  
   - Allowing `Access-Control-Allow-Origin: *` exposes sensitive APIs.

---

## 🛠 Attack Techniques
- URL/parameter manipulation (`id=101 → id=102`)  
- Cookie/JWT tampering (`role=user → role=admin`)  
- Modifying hidden form fields  
- Brute-forcing IDs or URLs  
- Direct API calls not exposed in the UI  

---

## 🔒 How to Prevent Broken Access Control
✔ **Deny by default** – Block all unless explicitly allowed.  
✔ **Enforce access control server-side** – Never trust the client.  
✔ **Role-Based / Attribute-Based Access Control** – Admins vs users.  
✔ **Use indirect references** – Replace sequential IDs with UUIDs.  
✔ **Audit & Pen-test** – Use tools like **Burp Suite, OWASP ZAP**.  

---

## 🧠 Real-World Examples
- **Facebook (2018):** IDOR allowed access to private posts.  
- **E-commerce sites:** Attackers changing order IDs to view others’ invoices.  

---

## ✅ Summary
- Broken Access Control = **most critical OWASP Top 10 risk**.  
- Attackers exploit weak/missing authorization checks.  
- Impacts: **data exposure, privilege escalation, full system compromise**.  

---
# 🔑 Broken Access Control & IDOR (Insecure Direct Object Reference)

---

## 📌 What is Access Control?
Access control ensures **who** (user, role, identity) can perform **what** (action, resource access) in a system.  
- **Authentication** → Verifies identity (login).  
- **Authorization** → Determines allowed actions.  

**Broken Access Control (BAC)** = Failure to properly enforce authorization rules, letting attackers do things they shouldn’t.  
👉 It is the **#1 risk in OWASP Top 10 (2021)** because it’s very common and dangerous.

---

## 🚨 Broken Access Control – Examples
1. **Insecure Direct Object References (IDOR)**  
   - User manipulates an object identifier (like `id=123`) to access another user’s data.  

2. **Privilege Escalation**  
   - A normal user becomes **admin** by tampering with a role value (`role=user → role=admin`).  

3. **Force Browsing**  
   - Accessing restricted URLs (`/admin`, `/deleteUser`) without proper checks.  

4. **Bypassing Access Controls**  
   - Calling APIs directly without verifying roles.  

5. **CORS Misconfigurations**  
   - Allowing `Access-Control-Allow-Origin: *` → sensitive APIs exposed.  

---

## 🛠 How Attackers Exploit BAC
- **URL manipulation** (`id=101 → id=102`)  
- **Cookie/JWT tampering** (`role=user → role=admin`)  
- **Hidden form field changes**  
- **Brute-forcing IDs / URLs**  
- **Direct API calls**  

---

## 🔒 How to Prevent Broken Access Control
✔ **Deny by default** – Block all unless explicitly allowed.  
✔ **Server-side enforcement** – Never trust the client.  
✔ **Role/Attribute-Based Access Control** – Assign strict privileges.  
✔ **Use indirect references** – Random UUIDs instead of sequential IDs.  
✔ **Audit & Pen-test** – Burp Suite, OWASP ZAP, manual testing.  

---

# 🔓 Insecure Direct Object Reference (IDOR)

## 📌 What is IDOR?
- **IDOR** is a subtype of **Broken Access Control**.  
- Occurs when applications expose **object references** (database IDs, filenames, keys) without proper authorization checks.  
- Attackers manipulate these values to access or modify **other users’ data**.  

👉 In simple terms: *“You can see other people’s stuff just by changing the number in the URL.”*

---

## 🧩 How IDOR Works
1. Application uses **user-controlled input** (URL, form field, parameter).  
2. System fetches the object **without validating ownership**.  
3. Attacker modifies the value → unauthorized access.  

---

## 🚨 IDOR – Examples
### 1. URL Parameter Manipulation
http
GET /account?id=101   → Your account
GET /account?id=102   → Another user’s account (if no check)
2. File Access
GET /files/invoice_1001.pdf   → Your invoice
GET /files/invoice_1002.pdf   → Someone else’s invoice
Booking/Order Manipulation
POST /cancelOrder
{
  "order_id": "12345"
}
4. API Exploitation
GET /api/v1/users/123/profile
🧠Real-World Cases of IDOR

Facebook (2018): Attackers accessed private posts/photos by manipulating object IDs.

Uber (2016): Researcher accessed invoices of other riders.

Indian Govt Portals: Aadhaar details leaked due to predictable IDs in URLs.
🛠 How Attackers Exploit IDOR

Manual testing: Guessing/changing IDs in URLs.

Fuzzing: Burp Intruder, ffuf to brute-force IDs.

Automation: Scripts to iterate through sequential object IDs.
🔒 Preventing IDOR

✔ Enforce access control server-side – Verify object ownership.
✔ Use indirect references – Replace sequential IDs with UUIDs/tokens.
✔ Deny by default – Only return objects belonging to authenticated user.
✔ Rate limiting & monitoring – Detect brute force attempts.
✔ Security testing – Regular pentests to catch IDOR.
⚡ Example: Secure vs Insecure

❌ Insecure
GET /user?id=105
✅ Secure
GET /user/profile
🧾 Final Summary

Broken Access Control = Weak/missing authorization → attackers gain unauthorized access.

IDOR = Direct object references (IDs, files, keys) exposed without validation.

Impact: Data leaks, account takeover, privilege escalation, system compromise.

Defense: Enforce server-side checks, deny by default, use indirect references, test regularly.
---
# Broken Access Control & IDOR

## 1. Broken Access Control

### Definition
Broken Access Control is a critical web application security risk that occurs when applications fail to enforce proper restrictions on what authenticated users can do. This vulnerability allows attackers to bypass authorization and gain access to resources or perform actions outside their intended permissions.

### Examples
- Accessing another user's account by changing the user ID in the URL.
- Modifying data without appropriate privileges.
- Accessing admin functionalities as a normal user.

### Common Issues
- **Insecure Direct Object Reference (IDOR)**
- **Missing Function Level Access Control**
- **Force Browsing** – Accessing pages without authentication.

### Impact
- Unauthorized data exposure (confidential information leaks).
- Data modification or deletion.
- Privilege escalation (normal user becoming admin).
- Complete compromise of application integrity.

### Mitigation
- Implement **server-side access control checks** for every request.
- Follow **principle of least privilege**.
- Use **deny by default** access policies.
- Avoid relying on security through obscurity (e.g., hidden URLs).
- Perform regular access control testing.

---

## 2. IDOR (Insecure Direct Object Reference)

### Definition
IDOR is a specific type of Broken Access Control vulnerability where an attacker manipulates input (like user ID, file ID, or record number) to directly access objects they are not authorized to access.

### Example
Suppose a banking application provides transaction details at:
```
https://bank.com/transactions?user_id=123
```
If the application does not validate whether the logged-in user owns `user_id=123`, an attacker can modify it to `user_id=124` and access another user's transactions.

### Real-World Example
- **Facebook Bug Bounty (2012):** Attackers could access private photos by manipulating object IDs in requests.
- **GitHub (2014):** A vulnerability allowed unauthorized access to private repositories.

### Impact
- Exposure of sensitive user data (PII, financial, health records).
- Account takeover or impersonation.
- Unauthorized file downloads or modifications.

### Mitigation
- Never trust user-supplied input for authorization.
- Implement **object-level authorization checks** on the server side.
- Use **randomized, non-sequential identifiers** (e.g., UUIDs instead of incremental IDs).
- Perform **penetration testing** to identify IDOR vulnerabilities.

---

## 3. Relationship Between Broken Access Control & IDOR

- **Broken Access Control** is the broader category of security flaws where access restrictions are not properly enforced.
- **IDOR** is a **subtype of Broken Access Control**, specifically involving direct references to objects (IDs, filenames, keys) without proper authorization checks.

### Analogy
- Think of **Broken Access Control** as an unlocked building with multiple rooms.
- **IDOR** is when someone enters another person’s room by simply changing the room number on the door.

---

## 4. Best Practices for Developers
- Enforce **authorization checks on every request** (not just authentication).
- Use **role-based or attribute-based access control models**.
- Log and monitor all access control failures.
- Educate developers about OWASP Top 10 vulnerabilities, especially **Broken Access Control** and **IDOR**.
 ---