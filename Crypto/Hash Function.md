# Hash Function

**Cryptographic Hash Function**

- Used to verify data integrity (checksumming)
- Store passwords
- Similar to BC; efficient to compute; one way function; avalanche; collision resistant.

**MD5 (message digest):** bad; chosen-prefix collision attachk which permit document forgery

**SHA-1:** less broken than MD5, time to move on. 512-bit blocks. The last block is appended with a 1 bit, some 0 bits and the message length.

- State is 160 bits (5 * 32 bit unsigned ints), initialized to values with fun hex rep const.
- For each 512-bit block: copy, perform bitwise operation on copy, xor. Output 160 bit.

**SHA-2,3:** longer output value, 256/512 bits. SHA-3 completely different design.

- Unique identifiers.
- Verifying message integrity.
- Storing passwords: salted hash. Hash (password + salt value) (at least 16 bytes random)

**HMAC (Keyed-Hash Message Authentication Code)**

- Hash (K || Hash(K || message)) concatenate
- K = secret key; don’t know = can’t forge HMAC