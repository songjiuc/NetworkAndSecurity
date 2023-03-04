# Symmetric Block Cypher

**Symmetric Cyphers:** the same secret key; shared securely beforehand; security depends on key size (how many bits long).

**Block Cyphers:** Algorithm for encrypting a fixed size block of data (block size is a property of the cypher). Produces a cyphertext (usually) the same size as the input block.

**Popular BC:** DES (Data Encryption Standard). 3DES, run DES 3 times. AES (Advanced Encryption Standard)

**Perfect cypher:** only way to break it is brute force.

K-bit key = 2^K possible keys = average guess half of those before correct = 2^(K-1).

**DES:** 64-bit block, 56-bit key (not big enough). A type of Feistel networks.

- Plaintext split into 2 halves. Broken up into several rounds. Each round uses a different round key which is based on secret key. F is a mangler function (don’t to be reversible, take 2 inputs produces 1 output). XOR to mix bits of the block, permute halves.
- Inefficient in software (bit swapping). Key-size/block size too small.
- 3 DES = E(D(E())).

**AES:** 128 bit block size. 128-192-256 bit keys. No of rounds depends on key size (also block size but fixed in standard). Efficient for software.

- 4x4 block grid of bytes: state; gets modified until it eventually becomes cyphertext
- SubBytes: substitute each byte in the state using a 256 entry table (defined)
- ShiftRows: permutation. For each I, rotate row I left by I columns. Except row 0
- MixColumns: permutation + xor. Table maps bytes to columns. For each column, for each row: look up the column for the entry, rotate it so its top is in the current row; xor all looked up columns together
- AddRoundKey (xor): xor the state with current round key.
- Like DES: each round gets a key derived from the secret key. Decryption is basically encryption in reverse.