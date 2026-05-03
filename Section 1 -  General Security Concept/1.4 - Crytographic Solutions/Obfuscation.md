## 1. Core Concept: Obfuscation
**Obfuscation** is the process of taking data that is normally easy to understand and making it difficult to interpret.
- **Key Characteristic**: The data is hidden in plain sight. If you know the specific method used to obfuscate it, you can reverse the process to retrieve the original information.
- **Security Limitation**: Relying solely on hiding the method is often called "security through obscurity," which is considered weak because the data can be recovered if the hiding method is discovered.

## 2. Steganography (Concealed Writing)
Derived from the Greek for "concealed writing," steganography involves hiding data within other forms of media known as **covertext**.
- **Image Steganography**: Data is embedded within an image file (e.g., using third-party utilities) without altering the visual appearance.
- **Network Traffic**: Messages can be hidden within TCP packets sent across a network.
- **Machine Identification Codes (MIC)**: Laser printers embed nearly invisible yellow dots on printed pages. These dots contain information about the specific printer and the time of printing.
- **Audio & Video**: Data can also be hidden within audio files or video tracks.

## 3. Tokenization
Tokenization is a method used daily in financial transactions where sensitive data is replaced with a non-sensitive substitute called a **token**.
- **How it Works**:
  1. **Registration**: A mobile device registers a credit card with a token service server and receives a unique token.
  2. **Transaction**: During payment (e.g., NFC), the device sends the token (not the actual card number) to the merchant.
  3. **Validation**: The merchant sends the token to the server, which maps it back to the real credit card number to validate funds.
  4. **Disposal**: The token is discarded immediately after the transaction, making it useless if intercepted.
- **Benefit**: Since the token has no mathematical relationship to the actual data, it can be transmitted without encryption, and intercepted tokens cannot be reused.

## 4. Data Masking
Data masking hides parts of sensitive information to prevent unauthorized access.
- **Common Usage**:
  - **Receipts**: Showing only the last four digits of a credit card (e.g., `****-****-****-1234`).
  - **Customer Service**: Representatives may only see partial numbers (e.g., "ending in 2512") to verify accounts without exposing the full number.
- **Techniques**: Hiding digits with asterisks, rearranging numbers, or substituting specific digits with others that can be reversed later if authorized.