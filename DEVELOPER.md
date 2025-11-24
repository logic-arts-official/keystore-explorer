# KeyStore Explorer - Developer Guide

Welcome to the KeyStore Explorer development team! This guide will help you get started with contributing to KSE.

---

## Table of Contents
1. [Quick Start](#quick-start)
2. [Development Environment Setup](#development-environment-setup)
3. [Project Structure](#project-structure)
4. [Building the Project](#building-the-project)
5. [Running and Debugging](#running-and-debugging)
6. [Testing](#testing)
7. [Code Style and Standards](#code-style-and-standards)
8. [Contributing](#contributing)
9. [Common Development Tasks](#common-development-tasks)
10. [Troubleshooting](#troubleshooting)

---

## Quick Start

Get up and running in 5 minutes:

```bash
# 1. Clone the repository
git clone https://github.com/kaikramer/keystore-explorer.git
cd keystore-explorer/kse

# 2. Build the project (requires Java 11+)
./gradlew build

# 3. Run the application
./gradlew run
```

That's it! KSE should launch with its GUI.

---

## Development Environment Setup

### Prerequisites

#### Required
- **Java Development Kit (JDK):** Java 11 or higher
  - Recommended: Java 17 or Java 21 LTS
  - Download from [Adoptium](https://adoptium.net/)
- **Git:** For version control
- **Gradle:** Included via wrapper (`gradlew`)

#### Recommended
- **IDE:** IntelliJ IDEA, Eclipse, or VS Code with Java extensions
- **IntelliJ IDEA Plugins:**
  - Resource Bundle Editor (for translations)
  - Gradle
  - CheckStyle-IDEA (for code style)

### IDE Setup

#### IntelliJ IDEA
1. **Import Project:**
   - File → Open → Select `kse` directory
   - Import as Gradle project
   - Use Gradle wrapper

2. **Configure Code Style:**
   - Download formatter: [kse_formatter.xml](https://keystore-explorer.org/kse_formatter.xml)
   - Settings → Editor → Code Style → Import Scheme
   - Select the downloaded XML file

3. **Set JDK:**
   - File → Project Structure → Project SDK
   - Select Java 11 or higher

#### Eclipse
1. **Import Project:**
   - File → Import → Gradle → Existing Gradle Project
   - Select `kse` directory

2. **Configure JDK:**
   - Project Properties → Java Build Path
   - Set JDK to 11 or higher

#### VS Code
1. **Install Extensions:**
   - Extension Pack for Java
   - Gradle for Java

2. **Open Project:**
   - File → Open Folder → Select `kse` directory

---

## Project Structure

```
keystore-explorer/
├── kse/                          # Main application directory
│   ├── build.gradle              # Build configuration (663 lines)
│   ├── gradle.properties         # Gradle properties
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── org/kse/
│   │   │   │       ├── KSE.java              # Main entry point
│   │   │   │       ├── crypto/               # Cryptographic operations
│   │   │   │       │   ├── csr/              # Certificate Signing Requests
│   │   │   │       │   ├── digest/           # Hash/digest algorithms
│   │   │   │       │   ├── keypair/          # Key pair utilities
│   │   │   │       │   ├── keystore/         # Keystore operations
│   │   │   │       │   ├── privatekey/       # Private key handling
│   │   │   │       │   ├── publickey/        # Public key handling
│   │   │   │       │   ├── secretkey/        # Secret key handling
│   │   │   │       │   ├── signing/          # Signing operations
│   │   │   │       │   └── x509/             # X.509 certificate utilities
│   │   │   │       ├── gui/                  # GUI components (359 files)
│   │   │   │       │   ├── actions/          # Menu/toolbar actions
│   │   │   │       │   ├── dialogs/          # Dialog windows
│   │   │   │       │   ├── error/            # Error handling UI
│   │   │   │       │   ├── preferences/      # User preferences
│   │   │   │       │   └── ...               # Other GUI packages
│   │   │   │       ├── utilities/            # Utility classes
│   │   │   │       └── version/              # Version information
│   │   │   └── resources/
│   │   │       └── org/kse/                  # Resource bundles, icons
│   │   └── test/
│   │       └── java/org/kse/                 # Unit tests (28 files, 993 tests)
│   ├── build/                    # Build output (generated)
│   ├── icons/                    # Application icons
│   ├── licenses/                 # License files for dependencies
│   ├── res/                      # Resources for distribution
│   ├── dmg/                      # macOS DMG resources
│   └── innosetup/                # Windows installer resources
├── .github/
│   └── workflows/                # GitHub Actions CI/CD
├── README.md                     # Project README
├── CONTRIBUTING.md               # Contribution guidelines
└── LICENSE                       # GPL v3 License
```

### Key Packages

| Package | Purpose | Files |
|---------|---------|-------|
| `org.kse` | Main entry point | 2 |
| `org.kse.crypto` | Cryptographic operations | ~100 |
| `org.kse.gui` | User interface | 359 |
| `org.kse.utilities` | Helper utilities | ~40 |

---

## Building the Project

### Basic Build

```bash
cd kse
./gradlew build
```

This will:
1. Compile all Java sources
2. Run all 993 unit tests
3. Create `build/libs/kse.jar`
4. Create distribution packages in `build/distributions/`

### Build Tasks

```bash
# Clean build
./gradlew clean build

# Build without tests
./gradlew build -x test

# Build only
./gradlew assemble

# Run tests only
./gradlew test

# Show all available tasks
./gradlew tasks --all
```

### Platform-Specific Builds

#### Windows Installer
```bash
./gradlew innosetup
# Requires InnoSetup 6 installed, ISCC.exe in PATH
# Requires Resource Hacker for exe customization
```

#### macOS Application Bundle
```bash
./gradlew appbundler
# Requires macOS
# Output: build/appBundle/KeyStore Explorer.app
```

#### macOS DMG
```bash
./gradlew dmg
# Requires macOS and create-dmg tool
```

#### Linux RPM Package
```bash
./gradlew buildRpm
```

#### Linux DEB Package
```bash
./gradlew buildDeb
```

#### Cross-Platform ZIP
```bash
./gradlew zip
# Works on Windows (generates kse.exe)
```

### Build Output

| Artifact | Location |
|----------|----------|
| Main JAR | `build/libs/kse.jar` |
| ZIP Distribution | `build/distributions/kse-<version>.zip` |
| TAR Distribution | `build/distributions/kse-<version>.tar` |
| Windows Installer | `build/distributions/kse-<version>.exe` |
| macOS DMG | `build/distributions/kse-<version>-x64.dmg` |
| Linux RPM | `build/distributions/kse-<version>.rpm` |
| Linux DEB | `build/distributions/kse-<version>.deb` |

---

## Running and Debugging

### Run from Command Line

```bash
# Using Gradle
./gradlew run

# Using Java directly (after building)
java -jar build/libs/kse.jar

# With specific keystore
./gradlew run --args="/path/to/keystore.jks"
```

### Run from IDE

#### IntelliJ IDEA
1. Open `org.kse.KSE.java`
2. Right-click → Run 'KSE.main()'
3. Or use the run configuration created automatically

#### Eclipse
1. Right-click on project
2. Run As → Java Application
3. Select `KSE - org.kse`

### Debugging

#### IntelliJ IDEA
1. Set breakpoints in code
2. Right-click `KSE.java`
3. Debug 'KSE.main()'

#### Command Line Debug
```bash
# Enable debug port 5005
./gradlew run --debug-jvm

# In IDE, attach remote debugger to localhost:5005
```

### JVM Options

Useful JVM options for development:

```bash
# Enable assertions
-ea

# Increase heap size
-Xmx2g

# Enable flight recorder
-XX:+FlightRecorder

# Debug security providers
-Djava.security.debug=provider

# Debug SSL/TLS
-Djavax.net.debug=ssl:handshake
```

---

## Testing

### Test Structure

```
src/test/java/org/kse/
├── crypto/
│   ├── csr/               # CSR tests
│   ├── digest/            # Digest/hash tests
│   ├── keypair/           # Key pair tests
│   ├── privatekey/        # Private key tests
│   ├── publickey/         # Public key tests
│   └── x509/              # X.509 certificate tests
└── utilities/             # Utility tests
```

### Running Tests

```bash
# Run all tests
./gradlew test

# Run specific test class
./gradlew test --tests DigestUtilTest

# Run with verbose output
./gradlew test --info

# Run with test report
./gradlew test
# Report: build/reports/tests/test/index.html
```

### Test Reports

After running tests, open the HTML report:
```
build/reports/tests/test/index.html
```

Statistics:
- **Total Tests:** 993
- **Success Rate:** 100%
- **Average Duration:** 8.5 seconds

### Writing Tests

#### Example Unit Test

```java
package org.kse.crypto.digest;

import org.junit.jupiter.api.Test;
import static org.assertj.core.api.Assertions.*;

class DigestUtilTest {
    
    @Test
    void testSha256Digest() {
        byte[] data = "Hello, World!".getBytes();
        byte[] digest = DigestUtil.sha256(data);
        
        assertThat(digest).hasSize(32);
        assertThat(digest).isNotEmpty();
    }
}
```

#### Test Best Practices

1. **Use JUnit 5** - Modern test framework
2. **Use AssertJ** - Fluent assertions
3. **Test One Thing** - Single responsibility per test
4. **Descriptive Names** - `testMethodName_condition_expectedResult`
5. **Arrange-Act-Assert** - Clear test structure
6. **Mock External Dependencies** - Use Mockito

### Test Coverage

Currently, there is no code coverage tool configured. **TODO: Add JaCoCo**

Recommended target: **70% code coverage**

---

## Code Style and Standards

### Code Formatting

#### Rules
- **Line Length:** Max 120 characters
- **Indentation:** 4 spaces (no tabs)
- **Braces:** Always use braces, even for single statements
- **Imports:** No wildcard imports

#### IntelliJ IDEA Formatter
Download and import: [kse_formatter.xml](https://keystore-explorer.org/kse_formatter.xml)

#### Example Code Style

```java
// Good
if (keyStore != null) {
    keyStore.load(inputStream, password);
    Certificate cert = keyStore.getCertificate(alias);
    return cert;
}

// Bad - no braces
if (keyStore != null)
    return keyStore.getCertificate(alias);

// Bad - too long
Certificate certificate = keyStore.getCertificate(aliasWithVeryLongNameThatExceedsOneHundredTwentyCharactersAndShouldBeWrapped);
```

### Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Classes | PascalCase | `KeyStoreUtil` |
| Interfaces | PascalCase | `CryptoProvider` |
| Methods | camelCase | `generateKeyPair()` |
| Variables | camelCase | `privateKey` |
| Constants | UPPER_SNAKE_CASE | `MAX_KEY_SIZE` |
| Packages | lowercase | `org.kse.crypto` |

### Documentation

#### JavaDoc Requirements

Document:
- All public classes
- All public methods
- Complex private methods
- Non-obvious code

```java
/**
 * Generates a new RSA key pair with the specified key size.
 *
 * @param keySize the size of the key in bits (e.g., 2048, 4096)
 * @return a new RSA key pair
 * @throws CryptoException if key generation fails
 */
public KeyPair generateRsaKeyPair(int keySize) throws CryptoException {
    // Implementation
}
```

### Git Commit Messages

Follow conventional commits:

```
type(scope): subject

body (optional)

footer (optional)
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Code style (formatting)
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance

**Examples:**
```
feat(crypto): add Ed25519 key generation support

fix(gui): resolve keystore save dialog crash on Windows

docs(readme): update build instructions for Java 21

test(crypto): add tests for ECDSA signature verification
```

---

## Contributing

### Workflow

1. **Fork the Repository**
   ```bash
   # On GitHub, click "Fork"
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/keystore-explorer.git
   cd keystore-explorer/kse
   ```

3. **Create a Branch**
   ```bash
   git checkout -b feature/my-new-feature
   ```

4. **Make Changes**
   - Write code
   - Add tests
   - Update documentation

5. **Test Your Changes**
   ```bash
   ./gradlew clean build
   ./gradlew test
   ```

6. **Commit**
   ```bash
   git add .
   git commit -m "feat(crypto): add new feature"
   ```

7. **Push**
   ```bash
   git push origin feature/my-new-feature
   ```

8. **Create Pull Request**
   - Go to GitHub
   - Click "New Pull Request"
   - Describe your changes

### PR Checklist

Before submitting a PR, ensure:

- [ ] Code builds successfully
- [ ] All existing tests pass
- [ ] New tests added for new functionality
- [ ] Code follows style guidelines
- [ ] No unrelated formatting changes
- [ ] Documentation updated if needed
- [ ] Commit messages are clear
- [ ] PR description explains the changes

---

## Common Development Tasks

### Adding a New Crypto Algorithm

1. **Create Algorithm Class**
   ```java
   // src/main/java/org/kse/crypto/keypair/NewAlgorithm.java
   package org.kse.crypto.keypair;
   
   public class NewAlgorithm {
       public static KeyPair generate(int keySize) {
           // Implementation
       }
   }
   ```

2. **Add Tests**
   ```java
   // src/test/java/org/kse/crypto/keypair/NewAlgorithmTest.java
   @Test
   void testGenerate() {
       KeyPair keyPair = NewAlgorithm.generate(2048);
       assertThat(keyPair).isNotNull();
   }
   ```

3. **Update GUI** (if needed)
   - Add to algorithm selection dialog
   - Update resources/messages

### Adding a New Keystore Format

1. **Implement KeyStore Provider**
   - Extend `KeyStoreSpi`
   - Register with `Security.addProvider()`

2. **Add Load/Save Support**
   - Update `KeyStoreUtil`
   - Add format detection

3. **Update GUI**
   - Add to format dropdown
   - Update file filters

### Internationalization

#### Adding a Translation

1. **Find Resource Bundle**
   ```
   src/main/resources/org/kse/gui/actions/resources.properties
   ```

2. **Create Language-Specific File**
   ```
   resources_XX.properties  # XX = language code
   ```

3. **Translate Strings**
   ```properties
   # resources.properties (English)
   action.newkeystore.name=New KeyStore
   
   # resources_de.properties (German)
   action.newkeystore.name=Neuer KeyStore
   ```

4. **Use Weblate** (Recommended)
   - Visit: https://hosted.weblate.org/projects/keystore-explorer/
   - Contribute translations online

### Adding Dependencies

1. **Update build.gradle**
   ```groovy
   dependencies {
       implementation('group:artifact:version')
   }
   ```

2. **Verify License Compatibility**
   - Must be compatible with GPL v3
   - Add license to `licenses/` directory

3. **Update Dependencies List**
   - Document in TECHNICAL_ANALYSIS.md

### Debugging Build Issues

```bash
# Clean build artifacts
./gradlew clean

# Show dependency tree
./gradlew dependencies

# Run with debug logging
./gradlew build --debug

# Run with stack traces
./gradlew build --stacktrace

# Show Gradle version
./gradlew --version
```

---

## Troubleshooting

### Build Fails: "Java version not supported"

**Problem:** Using Java version < 11

**Solution:**
```bash
# Check Java version
java -version

# Install Java 11+ from https://adoptium.net/
# Set JAVA_HOME
export JAVA_HOME=/path/to/java11
```

### Tests Fail: "Could not initialize class"

**Problem:** Crypto providers not available

**Solution:**
- Ensure BouncyCastle is in classpath
- Check for `bcprov-*.jar` in dependencies

### GUI Doesn't Start: "Graphics Environment"

**Problem:** Running on headless system

**Solution:**
```bash
# Enable headless mode for testing
java -Djava.awt.headless=true -jar kse.jar
```

### Build Slow: Gradle Downloading Dependencies

**Problem:** First build or cache cleared

**Solution:**
```bash
# Enable Gradle build cache
echo "org.gradle.caching=true" >> gradle.properties

# Use Gradle daemon
echo "org.gradle.daemon=true" >> gradle.properties
```

### IntelliJ IDEA: "Cannot resolve symbol"

**Problem:** IDE not synced with Gradle

**Solution:**
1. File → Invalidate Caches / Restart
2. Gradle panel → Reload Gradle Project
3. Build → Rebuild Project

---

## Additional Resources

### Documentation
- **README:** [README.md](README.md)
- **Contributing:** [CONTRIBUTING.md](CONTRIBUTING.md)
- **Technical Analysis:** [TECHNICAL_ANALYSIS.md](TECHNICAL_ANALYSIS.md)
- **Website:** https://keystore-explorer.org/

### Communication
- **GitHub Issues:** https://github.com/kaikramer/keystore-explorer/issues
- **GitHub Discussions:** https://github.com/kaikramer/keystore-explorer/discussions

### Related Tools
- **Keytool:** Java's CLI keystore tool
- **OpenSSL:** CLI crypto toolkit
- **BouncyCastle:** Java crypto library
- **Portecle:** Similar GUI tool (older)

---

## Quick Reference

### Essential Commands

```bash
# Build
./gradlew build

# Run
./gradlew run

# Test
./gradlew test

# Clean
./gradlew clean

# All tasks
./gradlew tasks
```

### Key Files

| File | Purpose |
|------|---------|
| `build.gradle` | Build configuration |
| `src/main/java/org/kse/KSE.java` | Main entry point |
| `src/main/resources/org/kse/version.properties` | Version info |
| `build/libs/kse.jar` | Compiled application |

### Key Classes

| Class | Package | Purpose |
|-------|---------|---------|
| `KSE` | org.kse | Application entry point |
| `KeyStoreUtil` | org.kse.crypto.keystore | Keystore operations |
| `X509CertUtil` | org.kse.crypto.x509 | Certificate utilities |
| `KeyPairUtil` | org.kse.crypto.keypair | Key pair utilities |

---

**Happy Coding! 🎉**

For questions, open a discussion on GitHub or check the [Contributing Guide](CONTRIBUTING.md).

---

**Last Updated:** June 10, 2024  
**Version:** 1.0
