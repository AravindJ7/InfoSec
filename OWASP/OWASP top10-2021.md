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
 # Injection

Injection flaws are very common in applications today. These flaws occur because the application interprets user-controlled input as commands or parameters. Injection attacks depend on what technologies are used and how these technologies interpret the input. Some common examples include:

## Types of Injection Attacks

### 1. SQL Injection
This occurs when user-controlled input is passed to SQL queries.  
As a result, an attacker can pass in SQL queries to manipulate the outcome of such queries.  
This could potentially allow the attacker to **access, modify, and delete information in a database** when this input is passed into database queries.  
An attacker could steal sensitive information such as **personal details and credentials**.

### 2. Command Injection
This occurs when user input is passed to system commands.  
As a result, an attacker can execute **arbitrary system commands** on application servers, potentially allowing them to access users' systems.

---

## Defence Against Injection Attacks

The main defence for preventing injection attacks is ensuring that **user-controlled input is not interpreted as queries or commands**. There are different ways of doing this:

### ✅ Using an Allow List
- When input is sent to the server, this input is compared to a list of **safe inputs or characters**.  
- If the input is marked as safe, then it is processed.  
- Otherwise, it is rejected, and the application throws an error.

### ✅ Stripping Input
- If the input contains **dangerous characters**, these are removed before processing.

---

## Dangerous Input
Dangerous characters or input is classified as any input that can **change how the underlying data is processed**.  

Instead of manually constructing allow lists or stripping input, various **libraries exist** that can perform these actions for you.
# Insecure Design

Insecure design refers to vulnerabilities that are inherent to the application's **architecture**.  
They are not caused by **bad implementations** or **misconfigurations**, but rather because the **concept or idea** behind the application (or part of it) is flawed from the start.  

Most of the time, these vulnerabilities occur when **improper threat modelling** is done during the planning phases of the application and propagate all the way up to the final product.  

Sometimes, insecure design vulnerabilities may also be introduced by developers while adding **shortcuts** for testing purposes.  
For example, a developer could disable OTP validation during development to speed up testing, but forget to re-enable it when sending the application to production.

---

## Example: Insecure Password Resets (Instagram Case)

A well-known example of insecure design was found in Instagram's password reset mechanism:  

- Users could reset forgotten passwords by receiving a **6-digit code** via SMS.  
- To brute-force such a code, an attacker would have to try **1,000,000 possible combinations**.  

### Bruteforce Limitation
- Instagram implemented **rate-limiting**: after **250 attempts per IP**, further attempts were blocked.  
- This should have made brute-forcing infeasible.  

### The Flaw
- The **rate-limit applied only per IP address**.  
- An attacker with access to multiple IPs could bypass the protection.  

### Distributed Bruteforcing
- With cloud services, attackers could cheaply rent thousands of IPs.  
- Example calculation:  
 
 - While 4,000 IPs may sound extreme, it was **feasible with cloud infrastructure**.  

---

## Why This Was Insecure Design
- The system’s design assumed that no user could distribute login attempts across thousands of IPs.  
- The flaw wasn’t in implementation (rate-limiting existed), but in the **core idea** of how the security model was designed.  
1,000,000 codes / 250 attempts per IP = 4,000 IPs required
---

## Mitigation & Prevention

Since insecure design vulnerabilities are introduced at such an **early stage**, fixing them often requires **rebuilding core parts** of the application — much harder than fixing simple code bugs.  

### Best Practices:
✔ Perform **threat modelling** early in the development lifecycle.  
✔ Anticipate **realistic attacker capabilities** (e.g., distributed attacks, cloud services).  
✔ Avoid relying on **single-point mitigations** (like IP-based rate limiting).  
✔ Use **multi-layered defences** (e.g., CAPTCHAs, device fingerprinting, risk-based authentication).  
 
 # Vulnerable and Outdated Components

## Overview
Vulnerable and outdated components are one of the most common security issues in web applications and systems. This occurs when organizations fail to update software, frameworks, libraries, or platforms to the latest versions, leaving them open to publicly known vulnerabilities. Attackers can exploit these weaknesses with minimal effort since many exploits are already available online.

---

## Example Scenario
Suppose a company is using **WordPress 4.6**, which has not been updated for years.  

- Using a tool like **WPScan**, a penetration tester can detect the version of WordPress.  
- Research shows that **WordPress 4.6** is vulnerable to an **unauthenticated Remote Code Execution (RCE)** vulnerability.  
- Exploits for this vulnerability are publicly available on sites like **Exploit-DB**, making it trivial for attackers to compromise the system.

This makes the situation extremely dangerous because:
1. The vulnerability is **well-known**.
2. Exploits are often **readily available**.
3. Attackers require **minimal skill or effort** to take advantage of the weakness.

---

## Why This Happens
- Organizations **miss updates** or patches due to:
  - Poor patch management.
  - Lack of monitoring.
  - Fear of downtime or breaking dependencies.
- Software and frameworks are often **not tracked properly**, leading to outdated versions running unnoticed.

---

## Risks
1. **Remote Code Execution (RCE):** Full system compromise.
2. **Privilege Escalation:** Gaining unauthorized access to higher-level accounts.
3. **Data Breaches:** Exposure of sensitive information.
4. **Denial of Service (DoS):** Exploiting old bugs to crash systems.
5. **Supply Chain Attacks:** Exploiting outdated third-party dependencies.

---

## Prevention
1. **Regular Updates & Patching**
   - Apply vendor patches and security updates immediately.
   - Use automated patch management systems.

2. **Software Inventory & Monitoring**
   - Maintain a list of all components, libraries, and frameworks.
   - Continuously monitor for new vulnerabilities (using CVE databases, NVD, or vulnerability scanners).

3. **Use Trusted Sources**
   - Only download components from official and verified repositories.

4. **Remove Unused Components**
   - Eliminate unnecessary plugins, libraries, or services that can introduce vulnerabilities.

5. **Vulnerability Scanning**
   - Use tools like **WPScan**, **Nessus**, or **OpenVAS** to identify outdated components.
   - Integrate vulnerability scanning into the CI/CD pipeline for DevSecOps.

---

## Key Takeaway
Even a **single missed update** can expose the entire system to catastrophic attacks. Keeping all components up-to-date and monitoring for known vulnerabilities is essential to maintaining security.

# Authentication and Session Management

Authentication and session management constitute core components of modern web applications. Authentication allows users to gain access to web applications by verifying their identities. The most common form of authentication is using a **username and password mechanism**. A user would enter these credentials, and the server would verify them. 

If successful, the server provides the users' browser with a **session cookie**. A session cookie is needed because web servers use HTTP(S) to communicate, which is stateless. Attaching session cookies ensures the server knows who is sending what data, allowing it to keep track of users' actions.

---

## Risks of Broken Authentication

If an attacker is able to find flaws in an authentication mechanism, they might successfully gain access to other users' accounts. This could allow the attacker to access sensitive data (depending on the purpose of the application).

### Common Flaws in Authentication Mechanisms

1. **Brute Force Attacks**
   - Attackers repeatedly attempt login with different username/password combinations.
   - Without protections, they can eventually guess valid credentials.

2. **Use of Weak Credentials**
   - Applications that allow weak or commonly used passwords (e.g., `password1`, `123456`) are vulnerable.
   - Attackers can easily guess these and gain unauthorized access.

3. **Weak Session Cookies**
   - Session cookies are used by the server to keep track of users.
   - If these cookies contain predictable values, attackers can forge their own cookies and hijack user sessions.

---

## Mitigation Strategies

1. **Strong Password Policy**
   - Enforce strong password requirements (minimum length, complexity, no common passwords).

2. **Brute Force Protection**
   - Implement account lockout or temporary blocking after multiple failed login attempts.

3. **Multi-Factor Authentication (MFA)**
   - Add an additional layer of verification such as SMS/email OTP, authenticator apps, or hardware tokens.

4. **Secure Session Management**
   - Use cryptographically secure, unpredictable session cookies.
   - Set secure cookie attributes like `HttpOnly`, `Secure`, and `SameSite`.
   - Implement session expiration and re-authentication for sensitive actions.

---

## Summary

Authentication and session management are critical for securing web applications. Poorly implemented mechanisms open the door to account takeover, data breaches, and other attacks. Strong credential policies, brute force protection, MFA, and secure session handling are essential defenses against **broken authentication vulnerabilities**.

# Integrity and Software/Data Integrity Failures

## What is Integrity?

In cybersecurity, **integrity** refers to the assurance that data remains unmodified and trustworthy. Maintaining integrity ensures that important data is free from unwanted or malicious changes.

For example, when downloading software, you want to ensure the installer wasn't tampered with or corrupted during transmission. To achieve this, software providers often include **hashes** (checksums) alongside their downloads.

A **hash** is the result of applying a mathematical algorithm (e.g., MD5, SHA1, SHA256) to a piece of data. Any small modification to the data produces a completely different hash value.

---

## Example: Verifying File Integrity with Hashes

Let's take **WinSCP** as an example. On its Sourceforge repository, developers publish the expected hashes for each file.

After downloading `WinSCP-5.21.5-Setup.exe`, you can calculate the file’s hashes on Linux:

```bash
user@attackbox$ md5sum WinSCP-5.21.5-Setup.exe          
20c5329d7fde522338f037a7fe8a84eb  WinSCP-5.21.5-Setup.exe
                                                                                                                
user@attackbox$ sha1sum WinSCP-5.21.5-Setup.exe 
c55a60799cfa24c1aeffcd2ca609776722e84f1b  WinSCP-5.21.5-Setup.exe
                                                                                                                
user@attackbox$ sha256sum WinSCP-5.21.5-Setup.exe 
e141e9a1a0094095d5e26077311418a01dac429e68d3ff07a734385eb0172bea  WinSCP-5.21.5-Setup.exe
```

Since the calculated hashes match the published ones, we can conclude that the file has **integrity** and has not been tampered with.

---

## Software and Data Integrity Failures

A **software or data integrity failure** occurs when applications rely on code or data without verifying its integrity. This can allow attackers to modify the code or data, leading to malicious outcomes.

### 1. Software Integrity Failures

Consider a website that includes **third-party libraries** hosted externally (e.g., jQuery):

```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
```

If attackers compromise the jQuery repository, they could inject malicious code. Since the website performs no integrity checks, users visiting the site would unknowingly execute the malicious code in their browsers.

✅ The solution is to use **Subresource Integrity (SRI)**, which ensures that browsers only execute the resource if its hash matches the expected value:

```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js" 
        integrity="sha256-o88AwQnZB+VDvE9tvIXrMQaPlFFSUTR+nldQm1LuPXQ=" 
        crossorigin="anonymous"></script>
```

You can generate SRI hashes at: [https://www.srihash.org/](https://www.srihash.org/)

### 2. Data Integrity Failures

This type of failure occurs when **data used by applications is not validated for integrity**. For example, configuration files, logs, or transmitted data could be altered by attackers if not protected with hashing or digital signatures.

---

## Summary

- **Integrity** ensures that data is unaltered and trustworthy.  
- **Hashes** are widely used to verify file integrity.  
- **Software Integrity Failures** happen when applications use third-party libraries without verifying them (solution: Subresource Integrity).  
- **Data Integrity Failures** occur when application data is not validated for tampering.  

Ensuring integrity is crucial for preventing malicious modifications in both software and data.
# Data Integrity Failures

## Overview
Data integrity failures occur when applications trust data that can be modified or tampered with by an attacker. Integrity mechanisms are essential to ensure that sensitive values (such as cookies, tokens, or session identifiers) have not been altered.

---

## Cookies and Session Management
When a user logs into an application, they are typically assigned a **session token** stored in the browser (commonly via cookies). The browser automatically sends this token with each subsequent request to maintain the session.

### Example: Weak Session Cookies
Suppose a webmail application assigns a cookie containing only the username after login.  
- If the user tampers with the cookie and changes the username, they could impersonate another user.  
- This constitutes a **data integrity failure** because the system trusts user-modifiable data.

---

## JSON Web Tokens (JWT)
A solution to ensure integrity is to use **JWTs (JSON Web Tokens)**. JWTs allow key-value pairs to be stored securely, with built-in integrity mechanisms.

### Structure of a JWT
A JWT consists of **3 base64-encoded parts**:
1. **Header** → metadata (e.g., type: JWT, algorithm: HS256)
2. **Payload** → claims or key-value pairs (e.g., username, expiry)
3. **Signature** → ensures payload integrity, generated using a secret key

If the payload is modified, the signature check fails unless the attacker has access to the secret key.

---

## JWT None Algorithm Vulnerability
Some vulnerable JWT libraries previously allowed attackers to bypass integrity checks by:  
1. Modifying the header to set `"alg": "none"`  
2. Removing the signature part  

### Example:
Original token:
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0IiwiZXhwIjoxNjY1MDc2ODM2fQ.C8Z3gJ7wPgVLvEUonaieJWBJBYt5xOph2CpIhlxqdUw

Tampered token with `"alg":"none"` and modified payload:
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJ1c2VybmFtZSI6ImFkbWluIn0.

This allows attackers to impersonate users such as `admin`.  

---

# Logging and Monitoring

## Importance of Logging
When applications are deployed, **every user action should be logged**. Logs are critical for:  
- **Incident response** → tracing attacker actions  
- **Regulatory compliance** → accountability in case of breaches  
- **Risk mitigation** → identifying further attacker presence  

### Information to Log
- HTTP status codes  
- Timestamps  
- Usernames  
- API endpoints / page locations  
- IP addresses  

Logs often contain sensitive data, so they must be securely stored, ideally with multiple backups.

---

## Suspicious Activity Detection
Monitoring helps detect unusual or malicious behavior. Examples include:  
- Multiple failed authentication attempts  
- Requests from unusual IPs or geolocations  
- Use of automated tools (detected via User-Agent headers or abnormal request frequency)  
- Known malicious payloads in requests  

### Risk-Based Response
Not all suspicious activity is equal. Activities should be assigned **impact levels**:  
- **High Impact** → e.g., repeated login failures, access to admin panels → should trigger alarms  
- **Medium/Low Impact** → less severe but still logged for investigation  

---

## Key Takeaways
- Integrity must be enforced on session tokens and sensitive data.  
- JWTs provide a reliable mechanism if implemented correctly.  
- Weak JWT implementations (e.g., allowing `alg: none`) are dangerous.  
- Logging and monitoring are essential for **detecting, investigating, and responding** to security incidents.  
