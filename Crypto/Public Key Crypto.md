# Public Key Crypto

**Diffie Hellman:** Agree on some public data.

- Modular arithmetic: clock arithmetic. Impossible to see how many time you’ve gone around the clock which makes the operation hard to reverse.
- Ta = g^Sa % n; Tb = g^Sb % n.
- Tb ^Sa % n; Ta ^Sb % n.
- Discrete logarithm problem.

**DHKE (Diffie Hellman Key Exchange):** The public keys (Ta, Tb) are shared in the open, while each person also keeps a “private key” to themselves (Sa, Sb). Anyone can know what the public keys are, but the private keys cannot be shared!

**RSA (Rivest-Shamir-Adleman):** similar to DH, rely on difficulty of discrete log problem. Mathier than DH

- Slower than symmetric crypto, often used for key exchange.
- Let us send messages, not just create keys.
- Public key = <e , n>; Private key = <d , n>; n = p-1 * q-1
- Encryption: message m is number < m.
- m^e % n, e and n are from Bob’s public key
- m = c^ d % n; m^(d*e)%n =m

**Signature with RSA:** sign a message by computing s = m^d % n; encrypt with your private key. People can verify by computing m = s^e % n

**Signed Certificates:** A certificate basically consists of info about the entity (company or website) and the entity’s public key. Cryptographically signed.

- Certificate authority: an entity that manages signed certificates.
- While communicating: ask for signed certificate, check the signature. If valid, repeat the process. Until verify one of the top level trust store certificates.