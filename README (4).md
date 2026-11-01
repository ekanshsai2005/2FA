# Two Factor Authentication Demo

A small web page that demonstrates how **two-factor authentication (2FA)** works.
A user must pass two checks to log in: something they **know** (a password) and a
one-time code (an OTP) that is generated for that login attempt.

> **Demo only.** This project is for learning. It is not secure and must not be used to protect real accounts (see [Security notes](#security-notes)).

## How it works

1. **Step 1: password.** The user enters the password. The demo password is `1234`.
2. **Step 2: OTP.** If the password is correct, the app generates a random 4-digit OTP and
   reveals the OTP field. The OTP is shown on screen as "Demo OTP", standing in for the SMS
   or authenticator app that would deliver it in a real system.
3. **Step 3: verify.** The user types the OTP. If it matches, the page shows **Login Successful ✔**.
   Otherwise it shows **Invalid OTP!**.

A wrong password shows **Wrong Password!** and keeps the OTP section hidden.

## Run it

No installation or internet connection is needed. Download `index.html` and double-click it to
open it in your browser.

**Try it:**
1. Enter `1234` and click **Login**.
2. Copy the 4-digit number shown as "Demo OTP".
3. Enter it and click **Verify OTP**.

## Technologies

- **HTML** for the page structure
- **CSS** for the card layout and gradient background
- **JavaScript** for the login and OTP logic (no libraries)

## Project structure

```
two-factor-auth-demo/
├── index.html   (page, styles and script)
└── README.md
```

## Code overview

| Part | What it does |
|---|---|
| `login()` | Checks the password. If it's correct, generates the OTP with `Math.floor(1000 + Math.random() * 9000)` and shows the OTP section |
| `verifyOTP()` | Compares the entered value with the generated OTP and shows a success or error message |
| `.success` / `.error` | CSS classes that colour the result message green or red |

## Security notes

This demo simplifies several things on purpose. A real 2FA system would differ in these ways:

- **Password:** it is hard-coded in the page source. Real systems store a salted hash on a server and never put it in client code.
- **OTP delivery:** the OTP is displayed on the same screen, which defeats the purpose of a second factor. Real systems send it through a separate channel (SMS, email or an authenticator app).
- **Client-side logic:** anyone can read or bypass JavaScript running in their own browser. Verification must happen on a server.
- **OTP generation:** `Math.random()` is not cryptographically secure; real systems use a secure generator or TOTP (RFC 6238).
- **Missing protections:** there is no expiry, attempt limit or rate limiting. Real OTPs expire in about 30 to 300 seconds and lock out after repeated failures.

## Ideas to extend it

- Add an OTP expiry timer (for example 30 seconds) and a "Resend OTP" button
- Limit attempts to 3 before locking the form
- Replace the on-screen OTP with an email OTP using a backend (Node.js or Flask)
- Implement TOTP, as Google Authenticator does
- Add a username field and store hashed passwords on a server
