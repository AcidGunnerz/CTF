# Old Sessions — picoCTF

- Category: Web Exploitation
- Platform: picoCTF

---

## Challenge Overview
The target web application features user registration, login functionality, and public posts. The challenge hints toward examining session handling mechanisms and potential session exposure endpoints across the site.

---

## Technical Analysis & Discovery
1. Initial Inspection & Reconnaissance:
   - Opened Browser Developer Tools (F12) to inspect DOM elements and application assets.
   - Examined static CSS assets (/static/login-register.css) for inline comments or hardcoded credentials; no actionable clues were present.

2. Application Interaction:
   - Registered a temporary testing account (username: acid, password: 1) to gain authenticated access to the dashboard.
   - Browsed public posts where challenge hints referenced a custom endpoint: /sessions.

3. Session Exposure Vulnerability:
   - Navigated directly to /sessions while authenticated.
   - The endpoint exposed active administrative session identifiers in cleartext, leaking the administrative token:
     VXuL_yhd9G8HcohJQ6hnJRykPXgsddpL4A5HIu0RQ

---

## Exploitation
1. Opened Developer Tools (F12) -> Application tab -> Cookies.
2. Modified the current session cookie value (session or PHPSESSID) to the leaked admin token:
   VXuL_yhd9G8HcohJQ6hnJRykPXgsddpL4A5HIu0RQ
3. Refreshed the page to hijack the admin session context.

### Flag Retrieval
academy{s3t_s3ss10n_3xp1rat10n5_3b59378b}

---

## Key Takeaways & Remediation
- Information Disclosure / Insecure Direct Object Reference (IDOR): Endpoints storing or displaying active session tokens (/sessions) must never be accessible to unauthenticated or low-privileged users.
- Session Invalidation & Expiration: Implement strict expiration times and invalidate session IDs upon logout or privilege escalation checks.