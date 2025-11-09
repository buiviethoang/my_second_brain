2025-11-04 21:56

TARGET DECK: [[security]]
START
Basic
Encode, Encrypt and Hash
Back:
## Main

### What? 
# Encode vs Encrypt vs Hash (quick map)

- **Encode / Decode**
    
    - Purpose: make data representable/transportable (not secret).
        
    - Examples: Base64, URL-encoding, hex, UTF-8.
        
    - Reversible easily (no secret needed). Use when you need safe transmission/storage of binary or special chars.
        
- **Encrypt / Decrypt**
    
    - Purpose: keep confidentiality. Reversible **only** with key(s).
        
    - Types: symmetric (AES — same key encrypt/decrypt) and asymmetric (RSA, ECIES — public/private key pair).
        
    - Use for private data in transit or at rest.
        
- **Hashing**
    
    - Purpose: fixed-size fingerprint; usually **one-way**.
        
    - Examples: SHA-256 (fast, general), bcrypt/scrypt/Argon2 (slow, salted — for passwords).
        
    - Use for verifying integrity (or passwords with a slow, salted hash).

# Common encoding examples (very lightweight)

- Base64: encode binary → ASCII safe (commonly used for attachments, tokens).
    
- URL-encoding: spaces → `%20`, etc.
    
- JSON serialization: not encryption — just representation.

# Authentication (AuthN) — verify _who_ you are

Common approaches:

- **Password-based**: username + password. Must store passwords as salted, slow hashes (Argon2 / bcrypt / scrypt / PBKDF2).
    
    - Never store plaintext or fast hashes (e.g., unsalted SHA).
        
- **Multi-factor auth (MFA)**: add TOTP (Google Authenticator), SMS (less secure), hardware keys (WebAuthn / FIDO2).
    
- **Token-based**:
    
    - **Session cookies** (traditional): server issues session ID, stored in a cookie (use `HttpOnly`, `Secure`, `SameSite`).
        
    - **JWTs (JSON Web Tokens)**: signed tokens containing claims. Useful for stateless auth, but beware of token revocation and storing sensitive info inside them.
        
- **OAuth2 / OpenID Connect**: delegated auth (log in via Google/SSO). OAuth is for authorization; OpenID Connect adds identity.
    
- **Certificate-based / Mutual TLS**: strong auth using client certs.
    
- **Passwordless & WebAuthn**: modern, phishing-resistant (public-key based).
    

# Authorization (AuthZ) — decide _what_ an authenticated user can do

- **Role-Based Access Control (RBAC)**: assign users roles (admin, editor, viewer) and map roles to permissions.
    
- **Attribute-Based Access Control (ABAC)**: policies use attributes (time, IP, resource attributes).
    
- **Permission checks**: always enforce server-side; never rely on client UI.
    
- **Least Privilege**: give minimum required permissions.
    

# Practical strategies & best practices

1. **Passwords**
    
    - Use Argon2 (preferred) or bcrypt/scrypt + unique salt per password + adequate parameters (memory/time).
        
    - Enforce strong password policies and rate-limit login attempts (account lockout or exponential backoff).
        
2. **Transport Security**
    
    - Always use HTTPS/TLS (no exceptions).
        
3. **Sessions & Tokens**
    
    - Cookies: set `HttpOnly`, `Secure`, `SameSite=Strict/Lax`. Use server-side session store for revocation.
        
    - JWTs: keep lifetime short (access token short, refresh token longer) and implement revocation via blacklist/rotation.
        
4. **MFA**
    
    - Offer TOTP or hardware-backed authentication.
        
5. **Key Management**
    
    - Protect private keys (HSM or cloud KMS). Rotate keys periodically & support key versioning.
        
6. **Input/output handling**
    
    - Encode output (HTML escape) to prevent XSS. Validate + sanitize inputs server-side.
        
7. **CSRF**
    
    - Use anti-CSRF tokens for state-changing requests, or use SameSite cookies and require Authorization headers.
        
8. **Rate limiting & brute force protection**
    
    - Rate-limit per IP and per account; add progressive delays or temporary lockouts.
        
9. **Audit & Logging**
    
    - Log auth events (logins, password changes, suspicious attempts) securely and monitor.
        
10. **Principle of least privilege**
    
    - Apply to services, databases, and users. Prefer separate service accounts with minimal permissions.
        
11. **Secure storage**
    
    - Secrets (API keys, DB passwords) in vaults not source code. Use environment variables + secret manager.
        
12. **Secure defaults**
    
    - Default to deny, require explicit allow. Fail securely.

## References
END

DELETE
ID: 
