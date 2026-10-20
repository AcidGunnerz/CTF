# Crack the Gate 1 — picoCTF

- Category: Web Exploitation
- Platform: picoCTF

---

## Challenge Overview
The challenge provides a target login page and specifies a target account email (ctf-player@cylabacademy.org). The objective is to bypass authentication or inspect application assets to access the administrative dashboard.

---

## Technical Analysis & Discovery
1. Initial Inspection & Source Code Analysis:
   - Opened Browser Developer Tools (F12) to inspect the application DOM and source code.
   - Identified a hidden comment within the frontend assets:
     ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf"

2. Decryption & Obfuscation Analysis:
   - Decoding the text via ROT13 yielded the developer note:
     NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"

---

## Exploitation
1. Intercepted the login request using Burp Suite and forwarded it to Repeater.
2. Appended the custom HTTP request header discovered in the developer comment:
   X-Dev-Access: yes
3. Sent the modified HTTP request, bypassing the password validation logic on the backend.

### Flag Retrieval
academy{brut4_f0rc4_b8c7f9c9}

---

## Key Takeaways & Remediation
- Sensitive Comments in Production: Never leave hardcoded developer notes, debugging flags, or temporary bypass mechanisms in client-facing HTML or JavaScript code.
- Insecure Header Trust: Backends must not rely on easily spoofable HTTP request headers (like custom X- headers) for critical authentication or privilege checks.