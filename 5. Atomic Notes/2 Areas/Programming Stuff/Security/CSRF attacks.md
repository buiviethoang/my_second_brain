2025-10-14 09:59

TARGET DECK: [[security]]
START
Basic
CSRF attacks
Back:
## Main

# What is CSRF?

**Cross-Site Request Forgery (CSRF)** is an attack that tricks a user’s browser into making an unwanted state-changing request (like changing email, transferring money, deleting data) to a site where the user is authenticated. The browser automatically includes credentials (cookies, basic auth) so the request looks legitimate to the target site.

# How it works (typical flow)

1. Alice is logged into `bank.example` (has a session cookie).
    
2. Alice visits `attacker.example`.
    
3. Attacker page contains a form or image/link that issues a request to `bank.example/transfer` (for example).
    
4. Browser sends the request to `bank.example` with Alice’s session cookie — the bank thinks Alice made the transfer.

# Key properties that make CSRF possible

- Browser sends credentials automatically (cookies, HTTP auth).
    
- The victim is authenticated on the target site.
    
- The site uses only cookie/session mechanisms for authentication and relies on predictable requests.


## References
END

DELETE
ID: 
