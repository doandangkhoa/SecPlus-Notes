# Advanced Encryption Standard (AES) Overview

## 1. Introduction and History
- **Purpose**: Replaced the Data Encryption Standard (DES) which had a short key length vulnerable to brute-force attacks.
- **Selection**: Chosen by NIST in 2001 from 5 finalists (MARS, RC6, Rijndael, Serpent, Twofish). The selected algorithm is **Rijndael**.
- **Block Size**: Fixed at **128 bits**.
- **Key Sizes**: Flexible; supports **128, 192, or 256 bits**.
- **Rounds**: The number of rounds depends on the key size:
  - 128-bit key: 10 rounds
  - 192-bit key: 12 rounds
  - 256-bit key: 14 rounds
- **Design Goals**: Provides **Diffusion** (spreading the influence of one bit over many) and **Confusion** (making the relationship between key and ciphertext complex).

## 2. Mathematical Foundation: Finite Fields (Galois Fields)
AES operations are performed on bytes, which are treated as elements of the finite field **GF(2⁸)**.

### Finite Field Properties
- **Elements**: Polynomials of degree at most 7 with coefficients in GF(2) (binary 0 or 1).
- **Addition**: Polynomial addition where coefficients are added modulo 2. This is equivalent to the **XOR** operation.
- **Multiplication**: Polynomial multiplication followed by **modulo** reduction with an irreducible polynomial.
- **Irreducible Polynomial (AES Standard)**:
  $$P(x) = x^8 + x^4 + x^3 + x + 1$$
  (Hex representation: `0x11B`)

### Inverse Operations
- Every non-zero element in GF(2⁸) has a multiplicative inverse.
- **Calculation**: To find the inverse of a byte, one can use the **Extended Euclidean Algorithm** or, more commonly in implementation, a pre-computed **Lookup Table**.
- **Example**: The inverse of `0xC2` (binary `11000010`) is `0x2F`.

## 3. AES Structure and Rounds
A 128-bit plaintext block is viewed as a $4 \times 4$ matrix of bytes (State). The encryption process consists of an initial **Key Addition**, followed by $N_r$ rounds, and a final round that omits the MixColumns step.
![](../../Images/Pasted%20image%2020260503231844.png)
### A. Key Addition (AddRoundKey)
- The current state is XORed with a round key derived from the main key via the **Key Schedule**.
- This step occurs before the first round and after every round.

### B. SubBytes (Substitution Layer)
- **Non-linear** substitution step.
- Each byte of the state is replaced by another byte using an **S-Box** (Substitution Box).
- **S-Box Construction**:
  1. **Multiplicative Inverse**: Calculate the inverse of the byte in GF(2⁸). (0 maps to 0).
  2. **Affine Transformation**: Apply a fixed linear transformation (matrix multiplication over GF(2)) followed by adding a constant vector.
- **Result**: Provides confusion.

### C. ShiftRows (Diffusion Layer)
- **Linear** operation.
- The state is treated as 4 rows. Each row is cyclically shifted to the **left** by a specific offset:
  - Row 0: Shift 0 (unchanged)
  - Row 1: Shift 1 byte
  - Row 2: Shift 2 bytes
  - Row 3: Shift 3 bytes
- **Result**: Bytes are moved between columns to ensure diffusion.

### D. MixColumns (Diffusion Layer)
- **Linear** operation.
- Operates on each column of the state independently.
- Each column (viewed as a polynomial of degree 3) is multiplied modulo $x^4 + 1$ by a fixed polynomial $c(x) = \{03\}x^3 + \{01\}x^2 + \{01\}x + \{02\}$.
- **Implementation**: Equivalent to matrix multiplication of the column vector by a fixed matrix over GF(2⁸):
  $$
  \begin{bmatrix}
  02 & 03 & 01 & 01 \\
  01 & 02 & 03 & 01 \\
  01 & 01 & 02 & 03 \\
  03 & 01 & 01 & 02
  \end{bmatrix}
  $$
- **Note**: This step is **omitted** in the final round of AES.

## 4. Performance and Implementation Notes
- **Speed**: Calculations on 64-bit registers (like `double` or `long long` in C++) are generally faster than bit-by-bit operations, but AES is optimized by operating on full bytes.
- **Optimization**:
  - **Lookup Tables**: Storing pre-computed S-Boxes and Inverse tables in memory is faster than calculating inverses using the Extended Euclidean Algorithm for every byte.
  - **Trade-off**: Using tables consumes more memory but reduces CPU cycles; using algorithms saves memory but increases computation time.
- **Real-world Context**: Efficient implementation is critical for real-time encryption (e.g., voice calls), where latency must be minimal.

## 5. Key Schedule (Brief Mention)
- The transcript notes that generating round keys from the master key is a distinct process (Key Schedule) that will be covered separately. It expands the initial key into a sequence of round keys used in the AddRoundKey step.
