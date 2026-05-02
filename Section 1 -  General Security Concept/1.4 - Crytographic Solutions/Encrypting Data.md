## 1. Encryption at Rest (Storage Devices)
Protecting data stored on physical media like SSDs and hard drives is known as **encrypting data at rest**.
- **Full Disk/Volume Encryption**: Encrypts the entire storage device.
  - **Windows**: Uses **BitLocker**.
  - **macOS**: Uses **FileVault**.
  - **Other OS**: Various built-in tools exist for volume-level encryption.
- **File-Level Encryption**: Encrypts specific files or folders without securing the whole volume.
  - **Windows**: Uses **EFS (Encrypting File System)**, accessible via file properties > Advanced Attributes.
  - **Cross-Platform**: Third-party utilities are available for macOS, Linux, and Windows.

## 2. Database Encryption
Databases often require specialized encryption techniques to balance security with performance.
- **Transparent Encryption**: Uses a **symmetric key** to encrypt the entire database.
  - *Pros*: Maximum security.
  - *Cons*: High overhead; the system must decrypt data every time it is accessed or searched.
- **Column-Level Encryption**: Encrypts only specific sensitive columns (e.g., Social Security Numbers) while leaving others (e.g., Names, IDs) in plain text.
  - *Pros*: Reduces overhead; allows fast searching on non-sensitive data.
  - *Cons*: Requires decryption only for the specific encrypted columns when accessed.

## 3. Network Encryption
Data transmitted across networks must be protected to prevent interception.
- **HTTPS**: Encrypts communication between a browser and a website.
- **VPNs (Virtual Private Networks)**: Create an encrypted "tunnel" for data.
  - **Client-to-Server**: Often uses **SSL** or **TLS**.
  - **Site-to-Site**: Often uses **IPsec**.

## 4. Encryption Algorithms and Compatibility
For successful communication, both parties must use the **same encryption algorithms**.
- **Algorithm vs. Key**:
  - **Algorithms** are public and well-known (e.g., the math behind them is transparent and trustworthy).
  - **Keys** are the secret component required to encrypt or decrypt data. Without the key, the algorithm alone cannot access the data (similar to knowing how a lock works but lacking the key).
- **Examples**:
  - **DES (Data Encryption Standard)**: An older algorithm with a 64-bit output.
  - **AES (Advanced Encryption Standard)**: A modern, more secure standard with various output versions.
  - *Note*: You cannot encrypt with DES and decrypt with AES; compatibility is essential.

## 5. Key Security and Brute Force Attacks
- **Brute Force Attacks**: Attackers attempt to guess keys by trying every possible permutation.
- **Defense Strategies**:
  - **Longer Keys**: Increasing key length makes brute force attacks computationally infeasible.
    - *Symmetric*: 128 bits or larger is standard.
    - *Asymmetric*: 3072 bits or larger is common due to complex prime number mathematics.
  - **Key Stretching (Key Strengthening)**: Applying the encryption or hashing process multiple times (e.g., hashing a password, then hashing the result again).
    - This significantly increases the time and computing power required for an attacker to succeed, adding a critical layer of security.