owasp, security, authentication

# Authentication

- [Authentication Best Practices](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Authentication_Cheat_Sheet.md)


## Authentication Protection
Use `Hashing`.

### Hashing
>The process of generating a unique value (`hash`) for a given text, string, or numberic input (key).

- one-way function =  must be irreversible
- each input should have a unique output
- generated `hash` can be text, string or numeric value, depending on the `Hash function` used

#### collision
> A scenario when a hash function gives the same output for different inputs.

#### Hashing Algorithms
- MD5 
    - NOT GODD, can be reversed by brute force attacks
    - high chance of collisions
    - fast
    - for non-critical applications only
- SHA (Secure Hash Algorithm)
    - includes SHA-0, SHA-1, SHA-2, SHA-3
    - more secure than MD5
    - high chance of collision but better than MD5
    - for general purpose applications with limited input (university portal)
- bCrypt
    - preferred choice of developers
    - used to generate user passwords
    - used for critical applications
    - uses iterative steps to generate the hash
- sCrypt
    - computationally intensive method


### Salting
> Approach to generate two different hash values for two different users provideing the same input.

- you do not force users to create uniuqe passwords, as you do not want to warn them the password is already in the system it would help hackers
- by using salt even if one user's password is compromised, it can be used to get into the other user's account (even if they have a same password and the hacker knows that fact)


How it works:
- must be done on the server
- salt is generated randomly, preferable different for each user
- for numeric salt values use secure algorithms like Cryptographically Secure Pseudo-Random Number Generator (CSPRNG)
- for alpha-numeric solt you can use Apache class