# Terminal Tool Documentation

# Table of Contents
 Overview
 Features
 Security Details
 Installation
 Dependencies
 Usage
 Code Documentation
 Examples
 Troubleshooting
 Security Considerations

# Project requirements:
Creating a Tool that should encyrpt and decrypt the files.
the tool should work on Linux, MacOs, Windows and Android.
when we encrypt the files it should generate a 7 letter code which includes numbers, charecters, special charecters.
when we decrypt the tool, if there is NN or MM modules in the 7 letter code, the tool should dynamically change the NN or MM to the date or month of file decryption. (ex: encyrption key : compaNN, then if the date of decrypiton is 20thOctober, the decryption key should be : compa20)
if there is any special charecter in encyrption key, the decryption key should invert the NN or MM module. (encryption key : comp/NN,then if the date of decryption is 20thOctober, the decryption key should be : comp/02 )

# Overview

 The Terminal Encryption Tool is a command-line application that provides secure file and directory encryption using AES-256 encryption. It supports both file and directory encryption/decryption, with a unique key management system that incorporates date-based validation.

# Features

 AES-256 encryption for files and directories
 User-specific key management
 Date-based key validation
 Support for both single file and recursive directory encryption
 Cross-platform compatibility (Windows, Linux, macOS)
 Metadata embedding for enhanced security

# Security Details


 Encryption Algorithm: AES-256 in CBC mode
 Key Derivation: PBKDF2 with SHA-256
 Initialization Vector: Random 16-byte IV for each encryption
 Padding: PKCS7 padding
 Metadata: 8-byte metadata embedded in encrypted files


# prerequisites.

Python 3.7 or higher
pip (Python package installer)
Docker desktop for windows and macos for docker image. 

 # Installation
 Install the required dependencies using pip:
 pip install cryptography pwinput
 
 Or create a virtual environment and install dependencies:

 python -m venv venv
 source venv/bin/activate  # On Windows, use: venv\Scripts\activate
 pip install cryptography pwinput

Steps to run python commands:

# Run the below python command using encryption_tool.py script to encrypt a file:

 python encryption_tool.py encrypt path/to/file

# Run the below python command using encryption_tool.py script to decrypt a file:

 python encryption_tool.py decrypt path/to/file.enc

# Run the below python command using encryption_tool.py script to encrypt a directory:

 python encryption_tool.py encrypt path/to/directory

# Run the below python command using encryption_tool.py script to decrypt a directory:

 python encryption_tool.py decrypt path/to/directory_enc

# Secret Key Format
 The key should be seven alphanumeric characters. You can include special date placeholders:

 MM: Will be replaced with the current month

 NN: Will be replaced with the current date

 if there are any special characters in the secret key, it will reverse the digits of the MM and NN.

Steps to execute the docker image:
# To build the docker image
   docker build -t imagename .
 # To run the docker image when we want to encrypt the file:
   docker run -it -v <path of the file>:/mnt <image name>  encrypt /mnt/<filename>
#  To run the docker image when we want to decrypt the file:
   docker run -it -v <path of the file>:/mnt <image name>  decrypt /mnt/<filename.enc>
#  To run the docker image when we want to encrypt and decrypt the folder:
   docker run -it -v <path of the folder>:/mnt <image name> encrypt /mnt/<foldername>
#  To run the docker image when we want to encrypt and decrypt the folder:
   docker run -it -v <path of the file>:/mnt <image name>  decrypt /mnt/<foldername_enc>

# Examples:

 Key: @3jcfA5 - Simple alphanumeric key
 Key: cjnsMMa - Uses current month
Key: @#$%!MM - Uses reversed current month
 Key: NN()jjc - Uses current date


# Code Documentation

Key Functions

 Generates an AES-256 key from the user's input key.

 Uses PBKDF2 with SHA-256
 100,000 iterations
 32-byte key length

 encrypt_file(file_path, key, remove_original=False)

 Encrypts a single file.

 Creates a new file with .enc extension
 Embeds metadata and IV in the encrypted file
 Uses AES-256 in CBC mode with PKCS7 padding


 decrypt_file(file_path, key, remove_enc=False)

 Decrypts an encrypted file.

 Extracts metadata and IV from the encrypted file
 Creates a new decrypted file


# Global Variables


 KEY_FILE: Path to the key storage file

 ENC_KEY: User's encryption key

 METADATA: Metadata string for encrypted files
# Examples

Example 1: Basic File Encryption

 $ python encryption_tool.py encrypt secret.txt
 Enter your key: \*\*A5bja
 Encrypted and copied: secret.txt -> secret.txt.enc



Example 2: Directory Encryption with Date-Based Key

 $ python encryption_tool.py encrypt documents/
 Enter your key: bahsMM2
 Encrypted directory and created a copy: documents/ -> documents_enc/

# Troubleshooting

 Common Issues and Solutions
 "Invalid key" error

 Ensure your key matches the format used during encryption
 Check if you're using the correct date-based key

 "Decryption failed" error

 Verify the file isn't corrupted
 Ensure you're using the correct key

 Permission errors
 Check if you have read/write permissions in the directory

#Security Considerations
 
 File Handling
 Original files can be optionally removed after encryption
 Encrypted files use .enc extension


