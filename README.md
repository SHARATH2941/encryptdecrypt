This tool provides a command-line interface for encrypting and decrypting files and directories using AES-256 encryption. It allows you to securely protect your files by generating encryption keys based on user input and ensures confidentiality by encrypting file contents.

Features

AES-256 Encryption: Uses the industry-standard AES-256 algorithm with CBC mode for secure encryption.
File Encryption: Encrypts individual files and appends a .enc extension.
Directory Encryption: Encrypts all files in a directory and creates an encrypted copy.
File Decryption: Decrypts encrypted files and restores their original contents.
Directory Decryption: Decrypts all files in an encrypted directory and creates a decrypted copy.
Metadata Handling: Includes metadata to validate keys and encryption details.
Key Management: Generates secure encryption keys and metadata based on user input.

Requirements
Python 3.6+
The following Python libraries:
cryptography
pwinput

To install the required libraries, run:
pip install cryptography pwinput

Installation
Clone this repository:
git clone <repository-url>
cd <repository-directory>

Ensure you have Python installed on your system.
Install the required dependencies.

Usage
The tool supports two main actions: encrypt and decrypt.
Encrypt Files or Directories

Command Syntax
python <script_name>.py encrypt <path_to_file_or_directory>

Example
Encrypt a file:
python tool.py encrypt /path/to/file.txt

Encrypt a directory:
python tool.py encrypt /path/to/directory

Notes
You will be prompted to enter a 7-character key for encryption.
Encrypted files will have a .enc extension.
Directories will have a copy created with _enc appended to the directory name.

Decrypt Files or Directories
Command Syntax
python <script_name>.py decrypt <path_to_file_or_directory>

Example

Decrypt a file:
python tool.py decrypt /path/to/file.txt.enc

Decrypt a directory:

python tool.py decrypt /path/to/directory_enc

Notes
You will be prompted to enter the decryption key used during encryption.
Decrypted files will have their original names, and directories will have _dec appended to their names.

Key Generation
The tool requires a 7-character key for encryption and decryption.
The key can contain alphanumeric characters and special characters.
The tool processes metadata to validate the encryption and decryption process.

Error Handling

Invalid paths will result in an error message.
If a wrong decryption key is provided, the tool will notify you of an invalid key.
Files and directories that fail encryption or decryption will remain unaffected.

Security Recommendations
Use strong, unpredictable 7-character keys.
Do not share your encryption key with untrusted parties.
Store backup copies of your encrypted files in a secure location.

License
This tool is open-source and available under the MIT License. Feel free to modify and use it according to your needs.

Disclaimer

This tool is provided as-is without any warranties. Use it at your own risk. The developers are not responsible for any data loss or misuse.
