## 1. What is a Cryptographic Hash?
A **cryptographic hash** (also known as a *message digest* or *fingerprint*) is a short string of text representing larger data.
- **Not Encryption**: You cannot recreate the original data from a hash, just as you cannot recreate a person from a fingerprint.
- **Primary Purpose**: To verify data **integrity**. If even one character in the input changes, the resulting hash changes completely.
- **Example (SHA256)**:
  - Input: `My name is Professor Messer.` → Hash A
  - Input: `My name is Professor Messer!` → Hash B (Completely different despite only one character change)

## 2. Collisions
A **collision** occurs when two different inputs produce the exact same hash.
- **Ideal Scenario**: Collisions should be extremely rare or non-existent.
- **MD5 Warning**: The **MD5** algorithm is no longer recommended because collisions were discovered in 1996. Different inputs can produce the same MD5 hash, compromising security.
- **SHA256**: A more secure algorithm producing 256 bits of information (represented as 64 hexadecimal characters).

## 3. Practical Applications of Hashing

### A. File Verification
When downloading files (e.g., Linux distributions), websites often provide a hash.
- **Process**: Download the file → Run the same hashing algorithm → Compare your result with the website's hash.
- **Result**: If they match, the file integrity is confirmed (it hasn't been tampered with).

### B. Password Storage
Passwords should never be stored in plain text or simply encrypted.
**Salting**: A random string of data (**salt**) is added to the password before hashing.
![](../../Images/Pasted%20image%2020260503134553.png)
  - **Benefit**: Even if two users have the same password (e.g., "dragon"), their stored hashes will differ because the salts are unique.
  - **Security**: This prevents attackers from using **Rainbow Tables** (pre-compiled lists of inputs and hashes) to reverse-engineer passwords instantly. It forces attackers to use brute-force methods, which take significantly longer.

## 4. Digital Signatures
Digital signatures provide **Integrity**, **Authentication**, and **Non-repudiation**.
- **Integrity**: Proves the message wasn't altered in transit.
- **Authentication**: Proves the message came from the claimed sender.
- **Non-repudiation**: The sender cannot deny sending the message.

### How a Digital Signature Works (Alice to Bob)
1.  **Creation (Alice)**:
    - Alice writes a message (Plaintext): *"You're hired, Bob."*
    - The system creates a **hash** of the message.
    - Alice's system **encrypts the hash** using her **Private Key**.
    - This encrypted hash is the **Digital Signature**, attached to the message.
2.  **Verification (Bob)**:
    - Bob receives the message and the signature.
    - His system **decrypts the signature** using Alice's **Public Key**, revealing the original hash.
    - Bob's system creates a **new hash** of the received message.
    - **Comparison**: If the decrypted hash matches the newly created hash, the signature is valid.
      - **Match**: The message is authentic and unaltered.
      - **Mismatch**: The message was tampered with or not sent by Alice.

> **Key Takeaway**: Digital signatures rely on the mathematical relationship between a private key (for signing) and a public key (for verification).
