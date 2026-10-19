# GET aHEAD — picoCTF (Web Exploitation)

- **Category:** Web Exploitation
- **Difficulty:** Easy
- **Platform:** picoCTF

---

## Challenge Overview
The target site presents a web page with two buttons: **GET** (which changes the background color to red) and **POST** (which changes the background color to blue). The challenge name **GET aHEAD** serves as the primary hint.

---

## Technical Analysis & Discovery
1. **Method Analysis:** Inspecting traffic in Burp Suite confirmed that sending `GET` or `POST` requests toggles presentation logic inside `index.php`.
2. **Vulnerability Identification:** The backend logic evaluates request methods using environment checks (`$_SERVER['REQUEST_METHOD']`). Failing to strictly validate incoming verbs leads to **HTTP Verb Tampering**.

---

## Exploitation
By sending an HTTP `HEAD` request instead of `GET` or `POST`, the server processes backend logic and returns custom response headers without rendering the body:

flag = picoCTF{r3j3ct_th3_du4l1ty_2e5ba39f}