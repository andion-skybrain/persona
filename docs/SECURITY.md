# Security Guide

This document outlines the security features and best practices implemented in the Persona application to protect your personal data.

## Overview

Persona is designed with security as a top priority. As a fully offline application, your data never leaves your device unless you explicitly export it. This provides an inherent level of security, as your data is not vulnerable to network-based attacks.

## Data Storage Security

### IndexedDB Storage

Persona uses IndexedDB for data storage, which provides:

- **Browser Sandboxing**: Each website's IndexedDB storage is isolated from other sites
- **Origin Binding**: Data can only be accessed by the same origin that created it
- **Local Storage**: All data remains on your device, not on external servers

### Data Encryption

Sensitive data can be encrypted using AES-256 encryption:

- **Financial Information**: Income, savings, investments
- **Health Information**: Medical conditions, medications
- **Personal Identifiers**: Social security numbers, ID numbers

When you encrypt data:
1. The data is encrypted using AES-256 algorithm
2. A unique encryption key is derived from your password using PBKDF2
3. A random salt is generated and stored with the encrypted data
4. The original data is removed from memory

To access encrypted data, you must provide the correct password. The password itself is never stored.

## Password Protection

### Persona Password Protection

Individual personas can be password-protected:

- Passwords are never stored in plain text
- Passwords are hashed using bcrypt with a work factor of 10
- Each password has a unique salt to prevent rainbow table attacks
- Failed password attempts are limited to prevent brute force attacks

### Profile Password Protection

User profiles can also be password-protected:

- Profile passwords use the same secure hashing as persona passwords
- Profile passwords protect all personas within that profile
- Master profile password is separate from individual persona passwords

## Input Validation & Sanitization

To prevent injection attacks and ensure data integrity:

- All user inputs are validated before processing
- Input validation includes type checking, length limits, and format validation
- Data is sanitized before storage to prevent XSS attacks
- HTML and script tags are escaped in text fields

## Import/Export Security

### Export Security

When exporting your data:

- Encrypted fields remain encrypted in the export file
- Password-protected personas require password verification before export
- Export files can be optionally encrypted with a password

### Import Security

When importing data:

- All imported data is validated for structure and content
- Malformed data is rejected to prevent corruption
- Encrypted data remains encrypted and requires the original password to decrypt

## Offline Security Benefits

Operating fully offline provides several security advantages:

- **No Network Exposure**: Data is not vulnerable to network-based attacks
- **No Server Vulnerabilities**: No server-side code that could be exploited
- **No Authentication Tokens**: No need for session tokens that could be stolen
- **Physical Device Security**: Data is only as vulnerable as your physical device

## Best Practices for Users

To maximize security:

1. **Use Strong Passwords**: Create complex passwords with a mix of characters
2. **Different Passwords**: Use different passwords for profiles and sensitive personas
3. **Regular Backups**: Export your data regularly and store backups securely
4. **Keep Application Updated**: Always use the latest version of Persona
5. **Secure Your Device**: Use device-level security (password/fingerprint) to protect access
6. **Private Browsing**: Consider using private/incognito mode for additional privacy

## Technical Security Implementation

For developers and technical users, here's how security is implemented:

### Password Hashing

```javascript
// Password hashing using bcrypt
const hashPassword = async (password) => {
  const salt = await bcrypt.genSalt(10);
  return bcrypt.hash(password, salt);
};

// Password verification
const verifyPassword = async (password, hash) => {
  return bcrypt.compare(password, hash);
};
```

### Data Encryption

```javascript
// Data encryption using AES
const encryptData = (data, password) => {
  const salt = CryptoJS.lib.WordArray.random(128/8);
  const key = CryptoJS.PBKDF2(password, salt, {
    keySize: 256/32,
    iterations: 1000
  });
  const encrypted = CryptoJS.AES.encrypt(JSON.stringify(data), key.toString());
  return {
    data: encrypted.toString(),
    salt: salt.toString(),
    timestamp: Date.now(),
    version: '1.0'
  };
};

// Data decryption
const decryptData = (encryptedData, password) => {
  const key = CryptoJS.PBKDF2(password, CryptoJS.enc.Hex.parse(encryptedData.salt), {
    keySize: 256/32,
    iterations: 1000
  });
  const decrypted = CryptoJS.AES.decrypt(encryptedData.data, key.toString());
  return JSON.parse(decrypted.toString(CryptoJS.enc.Utf8));
};
```

### Input Sanitization

```javascript
// Input sanitization to prevent XSS
const sanitizeInput = (input) => {
  return input
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#039;');
};
```

## Security Limitations

While Persona implements strong security measures, users should be aware of these limitations:

- **Device Security**: If someone has access to your unlocked device, they could access the application
- **Browser Vulnerabilities**: Browser-based vulnerabilities could potentially expose data
- **Export Files**: Exported files are only as secure as where you store them
- **Memory Limitations**: For technical reasons, some data may remain in memory temporarily

## Reporting Security Issues

If you discover a security vulnerability, please report it responsibly by:

1. Not disclosing the issue publicly until it has been addressed
2. Providing detailed information about the vulnerability
3. If possible, including steps to reproduce the issue

## Security Updates

Persona is regularly updated to address security concerns. Always use the latest version to ensure you have the most current security features.
