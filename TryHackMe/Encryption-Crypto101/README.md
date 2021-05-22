# 'Encryption-Crypto101' Room

## Notable learnings:

### Task 6:
  * The key variables that you need to know about for RSA in CTFs are p, q, m, n, e, d, and c.
  * “p” and “q” are large prime numbers, “n” is the product of p and q.
  * The public key is n and e, the private key is n and d.
  * “m” is used to represent the message (in plaintext) and “c” represents the ciphertext (encrypted text).
  * A [blog post](https://muirlandoracle.co.uk/2020/01/29/rsa-encryption/) to help understand RSA

### Task 7:
 * A [blog post](https://robertheaton.com/2014/03/27/how-does-https-actually-work/) on how HTTPS uses keys

### Task 9:
 * Introduced some cool John The Ripper techniques to crack `ssh` passwords using some wordlist

### Task 10:
 * An [explanation](https://www.youtube.com/watch?v=NmM9HA2MQGI) of how Diffie Hellman Key Exchange works
 * Main point is that DH Key Exchange often combined with RSA public key cryptography to prove identity of person you're talking to with digital signing.

### Task 11:
 * Used `gpg`. Good to note that you need to run `gpg --import [private-key]` in order to use `gpg --decrypt [encrypted-file]`
