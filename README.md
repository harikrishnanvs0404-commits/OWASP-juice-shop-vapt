# 🛡 OWASP Juice Shop – VAPT Assessment

Black-box web application penetration testing on OWASP Juice Shop demonstrating exploitation of SQL Injection, Cross-Site Scripting (XSS), Directory Exposure, and IDOR vulnerabilities.

---

## 📌 Assessment Overview

- **Target:** OWASP Juice Shop  
- **Testing Type:** Black-box Web Application Penetration Testing  
- **Tools Used:** Burp Suite, SQLmap, Dirsearch, Browser DevTools  
- **Total Findings:** 4  
  - Critical: 2  
  - High: 2  

---

## 🚨 Vulnerability Summary

| # | Vulnerability | Severity | CVSS |
|---|--------------|----------|------|
| 1 | SQL Injection | Critical | 9.8 |
| 2 | Cross-Site Scripting (XSS) | Critical | 9.0 |
| 3 | Exposed FTP Directory | High | 7.5 |
| 4 | Privilege Escalation (IDOR) | High | 8.0 |

---
1️⃣ SQL Injection – Authentication Bypass

POST /rest/user/login

💉 Payload Used
' OR 1=1--

📡 Intercepted Request (Burp)
POST /rest/user/login HTTP/1.1
Content-Type: application/json

{
  "email": "' OR 1=1--",
  "password": "test"
}

✅ Result

Authentication bypass successful.
JWT token returned.

💥 Impact

Complete authentication bypass

Admin account compromise

Potential full database exposure
2️⃣ Cross-Site Scripting (XSS)
🎯 Endpoint
#/search

💉 Payload
<script>alert('XSS')</script>

✅ Result

JavaScript executed in browser context.
💥 Impact

Session hijacking

Credential theft

Client-side attacks
3️⃣ Exposed FTP Directory
🎯 URL
/ftp

✅ Result

Directory listing enabled.
Files accessible without authentication.

💥 Impact

Information disclosure

Exposure of internal files

Increased attack surface
4️⃣ Privilege Escalation (IDOR)
🎯 Endpoint
GET /rest/basket/{id}

🛠 Exploitation Method

Login as normal user

Intercept request in Burp

Modify basket ID

Modified Request
GET /rest/basket/1
Authorization: Bearer <normal-user-token>

✅ Result

Access to another user's basket.

💥 Impact

Unauthorized data access

Privacy violation

Broken access control
🧠 Skills Demonstrated

Web Application Penetration Testing

Manual Exploitation Techniques

Burp Suite Interception & Manipulation

Injection Testing

Authorization Bypass Testing

Vulnerability Documentation

⚠ Disclaimer

This testing was conducted in a controlled lab environment using OWASP Juice Shop, an intentionally vulnerable application designed for security training.
