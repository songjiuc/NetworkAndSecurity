# Mode of Operation and Authentication

**Mode of Operation:** the way we use a block cypher to send a long message.

**Electronic code book:** send each block encrypted with the same key. Attackers can tell if repeated blocks are sent. Can rearrange blocks (move, delete).

**Cypher Block Chaining:** encrypt block using the same key. But, before encrypting a block, xor it with the previous cyphertext block. Xor the first message with a random block (initialization vector). Susceptible to bit flipping attacking at the expense of ruining the previous block of data. Less susceptible to block rearrangement attacks.

**Output Feedback mode:** use a BC to make a stream cypher. Make a random block and send it. Encrypt to get a block of pseudorandom data. Repeat to get a key stream.

**Counter Mode:** start with IV, encrypt IV+1 to get the first block of keystream.

**Galois Counter mode:** also computes a MAC to guarantee message integrity.

**Authentication Protocols**

**Shared secret-based protocols:**

- I’m alice
- R = Challenge / Nounce
- F(kab, R) = Encrypt/Hash
- Man in the middle offiline guess / session hijacking

**Minor tweak:**

- I’m alice
- Encrypt(R, Kab)
- R
- Offline guess; Alice authenticate Bob through kab.

**Time stamp:**

- Encrypt(timestamp, Kab)
- Timestamp
- Fewer messages but replay attack: send the same message to Bob and pretend to be Alice as long as the timestamp is recent enough.
- Use the key for multiple servers = add server name to prevent
- Or send timestamp + hash(timestamp + Kab) = high resolution clock without reversible E

**Public Key Crypto**

- I’m alice
- R
- Sign[R]
- Or
- I’m Alice
- Encrypt(R, Kab)
- R
- Sign whatever sent
- Encrypt whatever sent

**Mutual Authentication with Shared Secrets**

Requires both endpoints to prove their identities.

- I’m Alice
- R1
- F(Kab, R1), R2
- F(Kab, R2)
- Reflection attack if I’m alice R2
- Bod doesn’t send anything using Kab until Alice answer a challenge

**Mutual Authentication with public keys**

- I’m Alice, Encrypt(R2, Kbpub)
- Encrypt (R1, Kapub), R2
- R1