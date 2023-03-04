# Stream Cypher

**Stream Cyphers**: rarely 1 block sized message; stream of data; larger message. Stream of data XOR with a stream of random bits (key stream = one time pad).

CypherX = X xor K, CypherY = Y xor K; CypherX xor Cypher Y = X xor Y.

**Pseudorandome** numbers: appear random.

- Given k bits of the output, impossible for an attacker to know what the next bit will be.
- PRNG keeps track of some internal state. Impossible to know previous outputs.
- Period: the length of the PRNG sequence before it repeats. Long and unpredictable.

**RC4: Ron’s Code 4**

State is initialized using secret key. (Key schedule algorithm). Set the permutation to the identity. 

Initialization: J = 0; for I = 0 to 255; j = (j+s[i]+key[I % key length]) % 256; swap (s[i] s[j]).

```cpp
RC4::RC4(std::string password){
    // key is a shuffled array of uint8_t from 0 to 255
    Key key(password);
    
    // initialization
    for (int i = 0; i < 256; i++){
        s[i] = i;
    }
    
    int j = 0;
    for(int i=0; i<256; i++){
        j = (j+ s[i] + key.key_bytes[i % key.key_bytes.size()]) % 256;
        std::swap(s[i],s[j]);
    }
}
```

Next step: I = 0, j = 0; i++ % 256; j+= s[i] ; j % 256; swap (s[i], s[j]); output = s[(s[i] + s[j]) % 256]

```cpp
uint8_t RC4::get_next_byte(int i, int j){
    uint8_t byte = NULL;
    
    for(int n=0; n<s.size(); n++){
        i = (i + 1)%256;
        j = (j + s[i])%256;
        std::swap(s[i],s[j]);
        byte = s[(s[i] + s[j])%256];
    }
    return byte;
}

std::string encrypt_decrypt_rc4(std::string input, std::string password){
    RC4 rc4(password);
    std::string output;
    
    uint8_t key;
    uint8_t e_byte;
    int i =0;
    int j = 0;
    for(int x =0; x<input.length();x++){
        key = rc4.get_next_byte(i,j);
        e_byte = input.at(x) ^ key;
        output += e_byte;
    }
    
    return output;
}
```

ChaCha20: modern stream cypher of choice. add (unsigned int add with wraparound), rotate, xor. Nounce = number once; Stream position. Avoid accidental stream reuse.

**Bit Flipping Attacks:**

- Attacker knows part of the plaintext (where in the stream an important field is) = modify
- C = M xor K; X = M xor M’; M xor K xor M xor M’ = K xor M’; Get M’.
- Confidentiality but no data integrity.