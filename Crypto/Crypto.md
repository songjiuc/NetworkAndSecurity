# Crypto

**Cryptography** (also cryptology): secure communication in the presence of adversaries

**Cryptanalysis:** attempts to break cryptographic systems.

**Secure communication 4 Factors:**

- Confidentiality
- Data integrity
- Authentication
- Non-repudiation

**Adversaries:** eavesdropper, man in the middle, NSA-sized computers

**Symmetric:** if encryption and decryption use the same key. Faster.

**Asymmetric:** parties have a pair of keys: a public key which everyone knows about, and a private key which is secret. In practice, combine both.

**Cryptosystems:**

- Caesar Cypher: plaintext alpha char are rotated by an offset
- Pig Latin: the first letter is moved to the end of the word and concatenated with ay.

**Building blocks:** Efficient/feasible, reversible

- Substitution: replace parts of the message with something else
- Permutation: shift things around
- XOR (bitwise exclusive or): addition but better; a xor b xor b = a; independent bit.

**Types of attack:**

- Cyphertext only: self-explanatory
- Known plaintext: attacker somehow gets some plaintext/cyphertext pairs.
- Chosen plaintext: attacker somehow gets a party to encrypt some chosen plaintext

**Cyphertext should:**

- Appear random (otherwise susceptible to cyphertext only/known plaintext attacks)
- Avalanche effect small changes to input should result in large changes to cypher text. (Otherwise, susceptible to chosen plaintext attacks)
- Possible by combining 3 building blocks in various orders.

Perfect substitute = input + hash table/key = output; substitution table has an entry for each plaintext and contain all possible cyphertext outputs. Shuffle.

[Symmetric Block Cypher](Symmetric%20Block%20Cypher%2074e0078513704efa9e9b42fa524ebc26.md)

[Stream Cypher](Stream%20Cypher%20fe4db399c7124515825fbcfd3e162855.md)

[Hash Function](Hash%20Function%202b9070d61d2e4ecb94f5756c96d192d1.md)

[Public Key Crypto](Public%20Key%20Crypto%20c6513ce8b8754fa89b244d1179c11ee5.md)

[Mode of Operation and Authentication](Mode%20of%20Operation%20and%20Authentication%20065d262bb0644dbfa450ff7b84b7dae7.md)