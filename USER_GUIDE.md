# KeyStore Explorer - End-User Guide

**Version:** 5.6.0  
**Last Updated:** June 10, 2024

---

## Welcome to KeyStore Explorer!

KeyStore Explorer (KSE) is a free, open-source application that makes working with Java keystores, certificates, and cryptographic keys simple and intuitive. Whether you're a developer signing JAR files, a system administrator managing SSL certificates, or a security professional working with cryptographic keys, KSE provides a user-friendly interface to accomplish your tasks without memorizing complex command-line syntax.

---

## Table of Contents

1. [What is KeyStore Explorer?](#what-is-keystore-explorer)
2. [Getting Started](#getting-started)
3. [Key Features](#key-features)
4. [Common Tasks](#common-tasks)
5. [Understanding Keystores](#understanding-keystores)
6. [Working with Certificates](#working-with-certificates)
7. [Advanced Features](#advanced-features)
8. [Tips & Best Practices](#tips--best-practices)
9. [Troubleshooting](#troubleshooting)
10. [Frequently Asked Questions](#frequently-asked-questions)

---

## What is KeyStore Explorer?

### In Simple Terms

KeyStore Explorer helps you:
- **Manage Java keystores** - Store and organize your certificates and keys
- **View certificates** - See certificate details in a readable format
- **Generate keys** - Create new cryptographic keys easily
- **Sign JAR files** - Sign Java applications for distribution
- **Import/Export** - Move certificates and keys between different formats

### Why Use KeyStore Explorer?

Instead of typing complex commands like:
```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -keystore mykeystore.jks -storepass password
```

You can simply:
1. Click "Generate Key Pair"
2. Fill in a simple form
3. Done! ✅

### Who Uses KeyStore Explorer?

- **Java Developers** - Sign JARs, manage development certificates
- **System Administrators** - Manage server SSL/TLS certificates
- **DevOps Engineers** - Handle certificates for applications and services
- **Security Professionals** - Audit and manage cryptographic assets
- **Students** - Learn about certificates and cryptography

---

## Getting Started

### Installation

#### Windows
1. Download the installer from [GitHub Releases](https://github.com/logic-arts-official/keystore-explorer/releases)
2. Run the `.exe` installer
3. Follow the installation wizard
4. Launch KSE from the Start Menu or desktop shortcut

#### macOS
1. Download the `.dmg` file
2. Open the DMG
3. Drag "KeyStore Explorer" to Applications
4. Launch from Applications folder
5. If you see a security warning, go to System Preferences → Security & Privacy → Open Anyway

#### Linux
**Ubuntu/Debian:**
```bash
sudo dpkg -i kse_5.6.0_all.deb
kse
```

**Fedora/RHEL/CentOS:**
```bash
sudo rpm -i kse-5.6.0-1.noarch.rpm
kse
```

**Portable (Any Linux):**
```bash
tar -xzf kse-5.6.0.tar.gz
cd kse-5.6.0
./kse.sh
```

### System Requirements

- **Operating System:** Windows 10+, macOS 10.14+, or Linux
- **Java:** Java 11 or higher (bundled with installers)
- **Memory:** Minimum 512 MB RAM (1 GB recommended)
- **Disk Space:** 200 MB

### First Launch

When you first launch KSE:
1. You'll see the main window with an empty workspace
2. The menu bar at the top provides access to all features
3. The toolbar offers quick access to common operations
4. You're ready to create or open a keystore!

---

## Key Features

### 🗝️ Keystore Management
- Create new keystores in multiple formats
- Open existing keystores
- Save and backup keystores
- Convert between different keystore types
- Change keystore passwords

### 📜 Certificate Operations
- View certificate details
- Import certificates from files
- Export certificates to various formats
- Verify certificate chains
- View certificate extensions (X.509)

### 🔐 Key Generation
- Generate RSA key pairs (2048, 3072, 4096 bits)
- Generate ECC (Elliptic Curve) keys
- Generate DSA keys
- Create self-signed certificates
- Generate Certificate Signing Requests (CSRs)

### ✍️ Signing
- Sign JAR files for distribution
- Sign certificates
- Verify signatures

### 🔄 Import/Export
Support for multiple formats:
- PKCS#12 (.p12, .pfx)
- PKCS#8 (private keys)
- DER and PEM formats
- Microsoft PVK/SPC
- OpenSSL formats

### 🎨 User Interface
- Modern, intuitive design
- Drag-and-drop support
- Cut/copy/paste operations
- Dark mode support
- Multi-language support (8 languages)

---

## Common Tasks

### Task 1: Create a New Keystore

**When to use:** Starting a new project, need a place to store keys and certificates

**Steps:**
1. Click **File → New** (or press Ctrl+N / Cmd+N)
2. Choose keystore type:
   - **JKS** - Standard Java keystore (legacy)
   - **PKCS#12** - Modern, recommended for new keystores
   - **Other types** - For specific requirements
3. Click **OK**
4. You now have an empty keystore ready to use
5. Add entries (keys, certificates) as needed
6. Save the keystore: **File → Save** (Ctrl+S / Cmd+S)

**💡 Tip:** Use PKCS#12 for new keystores - it's the modern standard and more widely compatible.

---

### Task 2: Generate a Self-Signed Certificate

**When to use:** Development, testing, internal applications

**Steps:**
1. Open or create a keystore
2. Click **Tools → Generate Key Pair** (or Ctrl+G / Cmd+G)
3. Fill in the form:
   - **Algorithm:** RSA (recommended for most cases)
   - **Key Size:** 2048 bits (minimum), 4096 bits (more secure)
   - **Name:** Enter your name or organization
   - **Organization Unit:** Your department (optional)
   - **Organization:** Your company name
   - **Locality:** Your city
   - **State:** Your state/province
   - **Country:** Two-letter country code (e.g., US, GB, DE)
4. Set certificate **Validity** (e.g., 365 days)
5. Click **OK**
6. Enter an **alias** (name for this key pair)
7. Set a **password** for the key
8. Done! Your self-signed certificate is created ✅

**⚠️ Warning:** Self-signed certificates are NOT trusted by browsers. Use only for development/testing or internal applications.

---

### Task 3: Import a Certificate

**When to use:** Adding a trusted CA certificate, importing a certificate received from a Certificate Authority

**Steps:**
1. Open your keystore
2. Click **Tools → Import Trusted Certificate**
3. Click **Browse** and select the certificate file
   - Supported formats: .cer, .crt, .pem, .der
4. Review the certificate details
5. Click **OK** to import
6. Enter an **alias** for the certificate
7. Save the keystore

**💡 Tip:** You can also drag-and-drop certificate files directly into KSE!

---

### Task 4: Export a Certificate

**When to use:** Sharing your public certificate, backing up certificates

**Steps:**
1. Open your keystore
2. Right-click on the certificate entry
3. Select **Export → Export Certificate**
4. Choose export format:
   - **X.509** - Most common (.cer, .crt)
   - **PEM** - Text-based format
   - **DER** - Binary format
   - **PKCS#7** - Certificate chain
5. Choose location and save
6. Done! ✅

---

### Task 5: Sign a JAR File

**When to use:** Distributing Java applications, ensuring JAR integrity

**Steps:**
1. Open the keystore containing your signing key
2. Right-click on the key pair entry
3. Select **Sign JAR**
4. Click **Browse** and select the JAR file to sign
5. Choose signature algorithm (SHA256withRSA recommended)
6. Optionally, enter Timestamp Authority URL (recommended for long-term validity)
7. Click **OK**
8. Enter the key password if prompted
9. The JAR is now signed! ✅

**💡 Tip:** Always use a timestamp authority (TSA) when signing for distribution. This ensures signatures remain valid even after your certificate expires.

---

### Task 6: Generate a Certificate Signing Request (CSR)

**When to use:** Requesting a certificate from a Certificate Authority (CA)

**Steps:**
1. Open your keystore
2. Generate a new key pair (if you don't have one)
3. Right-click on the key pair entry
4. Select **Generate CSR**
5. Choose format:
   - **PKCS#10** - Most common, supported by all CAs
   - **SPKAC** - Netscape format (rare)
6. Review the CSR details
7. Save the CSR file (usually .csr or .pem)
8. Submit the CSR to your Certificate Authority
9. When you receive the signed certificate, import it back into this key pair entry

**📝 Note:** Keep the key pair in your keystore! You'll need it when the CA returns your signed certificate.

---

### Task 7: Convert Keystore Format

**When to use:** Need to use keystore with different applications, format compatibility

**Steps:**
1. Open your existing keystore
2. Click **Tools → Change Keystore Type**
3. Select the target format (e.g., JKS to PKCS#12)
4. Click **OK**
5. Save with a new name: **File → Save As**
6. You now have the keystore in the new format ✅

**Common Conversions:**
- **JKS → PKCS#12:** For modern applications
- **PKCS#12 → JKS:** For legacy Java applications
- **Any → BCFKS:** For FIPS compliance

---

### Task 8: View Certificate Details

**When to use:** Inspecting certificate information, verifying certificate validity

**Steps:**
1. Open your keystore
2. Double-click on any certificate entry
3. The certificate details window opens, showing:
   - **Subject:** Who the certificate is issued to
   - **Issuer:** Who issued the certificate
   - **Validity:** Start and end dates
   - **Public Key:** Algorithm and key details
   - **Signature:** Digital signature information
   - **Extensions:** X.509 v3 extensions (if any)
4. Click on tabs to see different views:
   - **Fields:** Detailed certificate fields
   - **Extensions:** Certificate extensions
   - **Public Key Details:** Key algorithm specifics
   - **PEM:** Text representation
5. Click **OK** to close

**💡 Tip:** Look for the "fingerprint" - it's a unique identifier for the certificate. Useful for verification!

---

## Understanding Keystores

### What is a Keystore?

A **keystore** is like a secure filing cabinet for your cryptographic keys and certificates. It stores:
- **Private keys** - Secret keys you must keep secure
- **Certificates** - Public certificates proving identity
- **Certificate chains** - Chains of trust from your certificate to root CAs

### Keystore Types

#### PKCS#12 (Recommended) 📦
- **File extensions:** .p12, .pfx
- **Standard:** International standard (PKCS #12)
- **Compatibility:** Works with most applications
- **Best for:** New keystores, cross-platform use
- **Security:** Good encryption

#### JKS (Legacy) 🏛️
- **File extensions:** .jks
- **Standard:** Java-specific
- **Compatibility:** Java applications only
- **Best for:** Legacy Java applications
- **Note:** Deprecated in favor of PKCS#12
- **⚠️ Migration recommended**

#### JCEKS (Java Crypto Extension)
- **Extension of JKS** with stronger encryption
- **Best for:** Storing secret keys
- **Java-specific**

#### BKS (BouncyCastle KeyStore)
- **File extensions:** .bks
- **Provider:** BouncyCastle
- **Versions:** V1, V2
- **Best for:** Android applications, BouncyCastle users

#### BCFKS (BouncyCastle FIPS)
- **FIPS-compliant** keystore
- **Best for:** Organizations requiring FIPS 140-2 compliance
- **Strong encryption**

#### UBER
- **BouncyCastle format**
- **Flexible keystore type**

### Choosing the Right Type

**For most users:** Use **PKCS#12**
- Modern standard
- Widely compatible
- Good security

**For Java-only apps:** Use **PKCS#12** or **JKS** (if required by legacy apps)

**For Android:** Use **BKS**

**For FIPS compliance:** Use **BCFKS**

---

## Working with Certificates

### Certificate Basics

A **certificate** is like a digital ID card. It contains:
- **Identity information** (name, organization, country)
- **Public key** (for encryption/verification)
- **Issuer** (who created the certificate)
- **Validity period** (not before / not after dates)
- **Digital signature** (proof it's authentic)

### Types of Certificates

#### 1. Self-Signed Certificate
- **Issued by:** You
- **Trusted by:** Only you (not browsers)
- **Use for:** Development, testing, internal tools
- **Cost:** Free

#### 2. CA-Signed Certificate
- **Issued by:** Certificate Authority (e.g., Let's Encrypt, DigiCert)
- **Trusted by:** Browsers, operating systems
- **Use for:** Production websites, public services
- **Cost:** Free (Let's Encrypt) or paid

#### 3. Root CA Certificate
- **Top of trust chain**
- **Pre-installed** in browsers/OS
- **Used to verify** other certificates

### Certificate Chain

A **certificate chain** shows the trust path:

```
Your Certificate
    ↓ (signed by)
Intermediate CA Certificate
    ↓ (signed by)
Root CA Certificate (trusted)
```

KSE shows certificate chains visually, making them easy to understand!

### Certificate Formats

| Format | Extension | Type | Description |
|--------|-----------|------|-------------|
| X.509 | .cer, .crt | Binary/Text | Standard certificate format |
| PEM | .pem | Text | Base64-encoded, human-readable |
| DER | .der | Binary | Compact binary format |
| PKCS#7 | .p7b, .p7c | Binary/Text | Certificate chain |
| PKCS#12 | .p12, .pfx | Binary | Certificate + private key |

**💡 Tip:** PEM format is text-based and can be opened in a text editor. Look for "-----BEGIN CERTIFICATE-----"

---

## Advanced Features

### Drag-and-Drop

KSE supports drag-and-drop for:
- **Certificates** - Drag .cer, .crt, .pem files into KSE
- **Keystores** - Drag .jks, .p12 files to open
- **Between keystores** - Drag entries between open keystores

### Copy/Paste/Cut

Manage entries like files:
1. Right-click an entry
2. Select **Copy** or **Cut**
3. Open another keystore (or the same one)
4. Right-click and select **Paste**
5. Entry is duplicated/moved!

### Certificate Extensions

X.509 v3 certificates can have extensions. View them by:
1. Double-click a certificate
2. Click the **Extensions** tab
3. See extensions like:
   - **Subject Alternative Name (SAN)** - Additional names/domains
   - **Key Usage** - What the key can be used for
   - **Extended Key Usage** - Specific purposes (e.g., TLS server)
   - **Basic Constraints** - Is this a CA certificate?

### Certificate Revocation Lists (CRL)

Create a CRL to revoke certificates:
1. Right-click a CA key pair
2. Select **Generate CRL**
3. Add revoked certificate serial numbers
4. Set CRL validity
5. Save the CRL

### Examine File

Quickly inspect a certificate or keystore file:
1. Click **Examine → Examine File**
2. Select a certificate or keystore file
3. View its contents without opening a keystore

### Detect File Type

Not sure what type of file you have?
1. Click **Examine → Detect File Type**
2. Select the file
3. KSE tells you what it is! (Certificate, keystore, CSR, CRL, etc.)

---

## Tips & Best Practices

### Security Best Practices

#### 1. Use Strong Passwords 🔒
- **Minimum:** 12 characters
- **Include:** Uppercase, lowercase, numbers, symbols
- **Avoid:** Dictionary words, personal information
- **Use:** Password manager to generate and store

#### 2. Backup Your Keystores 💾
- **Regular backups:** Weekly or after changes
- **Secure storage:** Encrypted drives, secure cloud storage
- **Test restores:** Verify backups work
- **Multiple copies:** Keep backups in different locations

#### 3. Protect Private Keys 🔐
- **Never share** private keys
- **Encrypt** keystores with strong passwords
- **Limit access** to keystores (file permissions)
- **Audit** who has access

#### 4. Certificate Expiration 📅
- **Track expiry dates** - Note when certificates expire
- **Renew early** - Start renewal 30-60 days before expiry
- **Set reminders** - Use calendar alerts
- **Future:** KSE will have built-in monitoring (roadmap!)

#### 5. Use Appropriate Key Sizes 🔑
- **RSA:** Minimum 2048 bits, prefer 4096 bits for long-term
- **ECC:** 256 bits minimum (equivalent to RSA 3072)
- **DSA:** Deprecated, avoid for new keys

#### 6. Timestamp When Signing ⏰
- Always use a **Timestamp Authority (TSA)** when signing
- Ensures signatures remain valid after certificate expiry
- Free TSAs available (e.g., Sectigo, GlobalSign)

### Performance Tips

#### 1. Close Unused Keystores
- Only keep needed keystores open
- Reduces memory usage
- Improves responsiveness

#### 2. Organize Your Keystores
- Use descriptive **aliases** for entries
- Group related certificates
- Document keystore purposes

#### 3. Regular Cleanup
- Remove expired certificates
- Delete unused key pairs
- Archive old keystores

### Workflow Tips

#### 1. Development vs Production
- **Separate keystores** for dev and prod
- **Label clearly** to avoid confusion
- **Different passwords** for each environment

#### 2. Certificate Lifecycle
```
1. Generate Key Pair
2. Create CSR
3. Submit to CA
4. Import Signed Certificate
5. Use certificate
6. Monitor expiration
7. Renew before expiry
8. Update applications
```

#### 3. JAR Signing Workflow
```
1. Create release keystore
2. Generate key pair (long validity, 10+ years)
3. Get CA certificate (optional but recommended)
4. Sign JARs with timestamp
5. Verify signature
6. Distribute
```

---

## Troubleshooting

### Common Issues

#### "Could not load keystore" ❌

**Cause:** Wrong password, corrupted file, or unsupported format

**Solutions:**
1. **Check password** - Verify keystore password is correct
2. **Try different types** - Try opening as different keystore type
3. **Check file integrity** - Ensure file isn't corrupted
4. **Restore from backup** - Use backup copy if available

---

#### "Incorrect password" ❌

**Cause:** Wrong password for keystore or key entry

**Solutions:**
1. **Verify password** - Check for typos, caps lock
2. **Try empty password** - Some keystores have no password
3. **Check documentation** - Look for password in project docs
4. **Reset if possible** - Some keystores allow password reset

---

#### "Certificate chain incomplete" ⚠️

**Cause:** Missing intermediate CA certificates

**Solutions:**
1. **Import intermediate certificates** - Get from CA, import to keystore
2. **Check CA website** - Download certificate bundle
3. **Verify chain** - Ensure all certificates in chain are present
4. **Use correct order** - Root → Intermediate → Your cert

---

#### "Certificate expired" ⏰

**Cause:** Certificate validity period has ended

**Solutions:**
1. **Renew certificate** - Get new certificate from CA
2. **Replace certificate** - Import renewed certificate
3. **Update applications** - Deploy new keystore to apps

---

#### "Cannot sign JAR" ❌

**Cause:** Missing private key, wrong entry type, or incorrect password

**Solutions:**
1. **Check entry type** - Must be key pair (not trusted certificate)
2. **Verify password** - Enter correct key password
3. **Check algorithm** - Ensure compatible signing algorithm
4. **Review key usage** - Certificate must allow code signing

---

#### Application hangs on startup 🐌

**Cause:** Large keystores, slow system, or Java issues

**Solutions:**
1. **Check Java version** - Ensure Java 11+ installed
2. **Increase memory** - Edit launch script, add `-Xmx1g`
3. **Clean Java cache** - Clear Java temporary files
4. **Reinstall** - Fresh installation may help

---

### Getting Help

#### Documentation
- **GitHub:** https://github.com/logic-arts-official/keystore-explorer
- **This Guide:** Keep for reference!

#### Community Support
- **GitHub Issues:** Report bugs, request features
- **GitHub Discussions:** Ask questions, share tips
- **Stack Overflow:** Tag questions with `keystore-explorer`

#### Reporting Bugs
When reporting a bug, include:
- **KSE version** (Help → About)
- **Operating system** and version
- **Java version** (Help → About)
- **Steps to reproduce**
- **Expected vs actual behavior**
- **Screenshots** if applicable

---

## Frequently Asked Questions

### Q: Is KeyStore Explorer free?
**A:** Yes! KSE is 100% free and open-source under GPL v3 license. Free for personal, commercial, and enterprise use.

### Q: Is it safe to use?
**A:** Yes! KSE is open-source, auditable, and has been trusted for 20+ years. Uses industry-standard BouncyCastle cryptography library.

### Q: Can I use it for commercial projects?
**A:** Absolutely! GPL v3 allows commercial use. No licensing fees or restrictions.

### Q: Does it work on Windows/Mac/Linux?
**A:** Yes! KSE is cross-platform and works on all three major operating systems.

### Q: Can I sign Android APKs?
**A:** Not directly, but you can manage the keystores used for signing. Use Android's `apksigner` tool for actual signing.

### Q: Can KSE replace keytool completely?
**A:** For most tasks, yes! KSE provides a GUI for 95% of keytool operations. Some advanced keytool features may still require command-line.

### Q: How do I contribute?
**A:** See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines. Code, documentation, translations, and bug reports all welcome!

### Q: Where are keystores stored?
**A:** Wherever you save them! KSE doesn't have a default location. Choose a secure location and remember where you save them.

### Q: Can I automate KSE?
**A:** Currently limited scriptability. Enhanced CLI and API are planned for 2027 (see [ROADMAP.md](ROADMAP.md)).

### Q: Does KSE support hardware security modules (HSM)?
**A:** Not yet, but HSM support is planned for 2026 (see [ROADMAP.md](ROADMAP.md)).

### Q: Can I use KSE with cloud key management (AWS KMS, Azure Key Vault)?
**A:** Not yet, but cloud integration is planned for 2025-2026 (see [ROADMAP.md](ROADMAP.md)).

### Q: Why should I use PKCS#12 instead of JKS?
**A:** PKCS#12 is the modern standard, more secure, and widely compatible. JKS is Java-specific and deprecated.

### Q: Can I recover a forgotten keystore password?
**A:** Unfortunately, no. Strong encryption makes password recovery impossible. Always backup your passwords securely!

### Q: How long should my certificate be valid?
**A:** Depends on use:
- **Development:** 1-2 years
- **Production websites:** 1 year (many CAs limit to 1 year now)
- **Code signing:** 3-10 years
- **Internal CA:** 10-20 years

### Q: Should I use RSA or ECC?
**A:** Both are secure:
- **RSA:** More compatible, larger keys (2048-4096 bits)
- **ECC:** More efficient, smaller keys (256-384 bits), faster
- **Recommendation:** RSA 4096 or ECC 256 for general use

---

## Glossary

**Alias** - A friendly name for an entry in a keystore

**CA (Certificate Authority)** - Organization that issues digital certificates

**Certificate** - Digital document proving identity, containing public key

**CSR (Certificate Signing Request)** - Request sent to CA to obtain certificate

**DER** - Binary encoding format for certificates

**DSA** - Digital Signature Algorithm (legacy, avoid for new keys)

**ECC (Elliptic Curve Cryptography)** - Modern, efficient public-key crypto

**JKS (Java KeyStore)** - Java's legacy keystore format

**Key Pair** - Public key + private key combination

**Keystore** - Secure storage for keys and certificates

**PEM** - Text-based encoding format (Base64)

**PKCS** - Public-Key Cryptography Standards

**Private Key** - Secret key that must be kept secure

**Public Key** - Shared key that can be distributed freely

**RSA** - Popular public-key cryptography algorithm

**Self-Signed** - Certificate signed by its own private key (not by CA)

**TSA (Timestamp Authority)** - Service that timestamps signatures

**X.509** - International certificate standard

---

## What's Next?

Now that you know the basics:

1. **Try it out!** Create a keystore, generate a key pair
2. **Explore features** - Click around, discover capabilities
3. **Read roadmap** - See what's coming: [ROADMAP.md](ROADMAP.md)
4. **Join community** - Contribute, ask questions, share feedback
5. **Stay updated** - Watch GitHub for new releases

---

## Additional Resources

### Learning Resources
- **Java Keytool Docs:** Oracle Java documentation
- **X.509 Certificates:** Wikipedia article on X.509
- **PKI Basics:** Public Key Infrastructure introduction

### Related Tools
- **Keytool:** Java's command-line keystore tool
- **OpenSSL:** Swiss army knife of cryptography
- **Certbot:** Let's Encrypt certificate automation
- **mkcert:** Local development certificates

---

**Need Help?**

🐛 **Found a bug?** Open an issue: https://github.com/logic-arts-official/keystore-explorer/issues  
💬 **Have a question?** Start a discussion: https://github.com/logic-arts-official/keystore-explorer/discussions

---

**Happy Keystoring! 🔐✨**

---

**Document Version:** 1.0  
**Last Updated:** June 10, 2024  
**For KSE Version:** 5.6.0
