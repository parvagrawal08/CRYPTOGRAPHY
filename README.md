# Cryptography — AES & DES Ciphers From Scratch

Pure Python implementations of **AES-128** and **DES** encryption algorithms, built entirely from scratch with zero external dependencies. Created for academic exploration of symmetric-key cryptography.

---

## Algorithms Overview

| Feature | AES-128 | DES |
| :--- | :--- | :--- |
| **File** | `AESCipher.py` | `DESCipher.py` |
| **Structure** | Substitution-Permutation Network (SPN) | Feistel Network |
| **Block Size** | 128 bits (16 bytes) | 64 bits (8 bytes) |
| **Key Size** | 128 bits | 56 bits effective (64-bit input) |
| **Rounds** | 10 | 16 |
| **Padding** | PKCS#7 | PKCS#7 |
| **Mode** | ECB | ECB |

---

## Repository Structure

```
CRYPTOGRAPHY/
├── AESCipher.py   # AES-128 encryption & decryption
├── DESCipher.py   # DES encryption & decryption
└── README.md
```

---

## Prerequisites

- **Python 3.6+**
- No external packages required

---

## Usage

### AES Cipher

```bash
python AESCipher.py
```

**Encryption:**
```
Mode (encrypt/decrypt): encrypt
Enter key (any text): mysecretpassword
Enter text to encrypt: Hello World!
Encrypted (hex): 7d81a8c3e808ce5bc6c887ba5bf54a2a
```

**Decryption:**
```
Mode (encrypt/decrypt): decrypt
Enter key (any text): mysecretpassword
Enter hex ciphertext: 7d81a8c3e808ce5bc6c887ba5bf54a2a
Decrypted: Hello World!
```

---

### DES Cipher

```bash
python DESCipher.py
```

**Encryption:**
```
Mode (1 for encryption / 2 for decryption): 1
Enter key (any text): secret8k
Enter text to encrypt: Hello World!
Encrypted (hex): a0199e4b78ca9013c72719a93325e0bc
```

**Decryption:**
```
Mode (1 for encryption / 2 for decryption): 2
Enter key (any text): secret8k
Enter hex ciphertext: a0199e4b78ca9013c72719a93325e0bc
Decrypted: Hello World!
```

---

## Programmatic Usage

Both ciphers can be imported and used in your own Python scripts:

### AES

```python
from AESCipher import aes_encrypt, aes_decrypt

key = b"mysecretkey12345"
ciphertext = aes_encrypt("Confidential data", key)
print("Encrypted:", ciphertext.hex())

plaintext = aes_decrypt(ciphertext, key)
print("Decrypted:", plaintext)
```

### DES

```python
from DESCipher import des_encrypt, des_decrypt

key = b"8bytekey"
ciphertext = des_encrypt("Secret message", key)
print("Encrypted:", ciphertext.hex())

plaintext = des_decrypt(ciphertext, key)
print("Decrypted:", plaintext)
```

---

## Implementation Details

### AES-128 (`AESCipher.py`)

- **Key Expansion**: Generates 11 round keys from a 128-bit key using S-Box substitution and Rcon XOR
- **SubBytes**: Non-linear byte substitution using a precomputed S-Box (and inverse for decryption)
- **ShiftRows**: Cyclic row shifts in the 4×4 state matrix
- **MixColumns**: Column mixing via Galois Field GF(2^8) multiplication
- **AddRoundKey**: XOR of state with the round key

### DES (`DESCipher.py`)

- **Key Schedule**: 64-bit key → PC-1 permutation → 56-bit key split into two 28-bit halves → 16 subkeys via left shifts and PC-2 permutation
- **Initial & Final Permutation**: IP and FP bit-level permutations on the 64-bit block
- **Feistel Function**: Expansion (E), XOR with subkey, 8 S-Box lookups (6→4 bit), and P-box permutation
- **16 Feistel Rounds**: Left and right halves swapped and XORed each round

---

## Disclaimer

These implementations are for **educational purposes only**. For production use, rely on vetted libraries such as [cryptography](https://cryptography.io/) or [PyCryptodome](https://pycryptodome.readthedocs.io/).
