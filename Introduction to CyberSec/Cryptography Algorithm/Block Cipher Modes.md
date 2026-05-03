## Key Concepts

### 1. Ideal Block Cipher & Key Usage
- **Ideal Block Cipher**: With a secret key, the encryption function acts as a random permutation.
- **Single-Use vs. Multi-Use Keys**: 
  - The lecture focuses on **multi-use keys** (e.g., encrypting an entire hard drive or multiple network packets with the same key), as managing unique keys for every file is impractical.

### 2. Electronic Codebook (ECB) Mode
- **Mechanism**: The message is split into independent blocks ($x_0, x_1, \dots$), and each is encrypted separately with the same key ($y_i = E_k(x_i)$).
- **Padding**: If the message length isn't a multiple of the block size, padding is added (e.g., appending a `1` followed by `0`s).
- **Critical Flaw**: ECB is **deterministic**. Identical plaintext blocks produce identical ciphertext blocks.
  - *Example*: Encrypting an image of the Linux penguin in ECB mode still reveals the outline of the penguin in the ciphertext because identical pixel blocks result in identical encrypted blocks.
  - *Attack Scenario*: An attacker (Oscar) can perform a **block substitution attack** in banking protocols. By capturing a valid transaction block (e.g., a specific account number block) and swapping it into a new transaction, they can redirect funds without knowing the key.
- **Conclusion**: ECB is **not secure** for structured data and should only be used for random data (like keys).

### 3. Probabilistic Encryption
- To ensure security, encryption must be **probabilistic**: Encrypting the same message twice with the same key should yield **different** ciphertexts.
- **Implementation**: Introduce randomness (e.g., a random number $R$) into the process. The ciphertext becomes a pair $(R, C)$, where $C = E_k(R) \oplus M$.
- **Benefit**: Prevents attackers from identifying repeated messages or patterns.

### 4. Cipher Block Chaining (CBC) Mode
![](../../Images/Pasted%20image%2020260503233856.png)
- **Mechanism**: Introduces an **Initialization Vector (IV)**.
  - $y_0 = E_k(x_0 \oplus IV)$
  - $y_i = E_k(x_i \oplus y_{i-1})$
- **Properties**:
  - **Probabilistic**: Requires a unique, random IV (or a nonce) for every encryption.
  - **Diffusion**: Changing one bit in the plaintext affects all subsequent ciphertext blocks.
  - **Decryption**: Can be parallelized, but encryption cannot.
  - **Padding**: Requires specific padding rules (e.g., PKCS#7) if the message isn't block-aligned.
- **Error Propagation**: If a ciphertext block is lost or corrupted during transmission, the corresponding plaintext block and the *next* block will be corrupted. (Losing block $L/2$ destroys $x_{L/2}$ and $x_{L/2+1}$).

### 5. Other Modes
- **Output Feedback (OFB)**: Turns the block cipher into a stream cipher.
  - Generates a keystream by repeatedly encrypting the IV (or previous output).
  - $y_i = x_i \oplus E_k(\text{previous output})$.
  - No padding required; errors do not propagate beyond the specific bit.
- **Cipher Feedback (CFB)**: Similar to OFB but the previous *ciphertext* block is fed back as input. Also acts as a stream cipher.
- **Counter (CTR) Mode**:
  - Uses a unique nonce and a counter (e.g., $Nonce, Counter, Counter+1, \dots$).
  - Encrypts the counter value to generate a keystream: $y_i = x_i \oplus E_k(Nonce || Counter)$.
  - **Advantages**: 
    - Highly efficient and supports **parallel encryption and decryption**.
    - No padding needed.
    - **Error Isolation**: Losing one ciphertext block only affects that specific plaintext block (unlike CBC).
  - **Current Standard**: CTR is widely used in modern systems due to its speed and security properties.

## Practical Exercise & Discussion
- **Case Study**: The professor discussed a hypothetical banking attack using ECB to illustrate why identical blocks are dangerous.
- **Assignment**: Students are tasked with implementing AES with **CBC** and **CTR** modes to encrypt files, comparing their performance and security characteristics.
- **Midterm**: Discussed potential formats (paper-based vs. project-based) and the timeline.

## Conclusion
The lecture emphasizes that **ECB is insecure** for general use due to pattern preservation. Modern secure systems rely on modes like **CBC** (with proper IV handling) or **CTR** (preferred for parallelism and error isolation) to convert deterministic block ciphers into secure, probabilistic encryption schemes.