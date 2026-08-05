# Android Mobile Banking Application - Static Security Assessment

A comprehensive Static Application Security Testing (SAST) and Reverse Engineering assessment performed against the intentionally vulnerable **VulnBank3** Android application.

This project demonstrates the complete workflow of analyzing an Android application to identify security weaknesses, reverse engineer application logic, recover hidden assets, and map the application's attack surface using industry-standard tools and methodologies.

---

# Objectives

The primary objectives of this assessment were to:

- Perform static analysis of the APK.
- Reverse engineer Android components.
- Inspect the AndroidManifest configuration.
- Analyze Java and Smali source code.
- Reverse engineer Hermes Bytecode.
- Discover hardcoded credentials and secrets.
- Enumerate exposed API endpoints.
- Identify insecure storage mechanisms.
- Review security misconfigurations.
- Map findings against OWASP MASVS.
- Produce a professional technical security assessment report.

---

# Assessment Workflow

The assessment followed a structured methodology consisting of multiple analysis phases:

### 1. APK Decompilation

- Decompiled the application using APKTool.
- Extracted application resources.
- Parsed AndroidManifest.xml.
- Generated Smali source files.

---

### 2. Java Source Analysis

Using JADX:

- Reviewed application architecture.
- Identified sensitive classes.
- Traced authentication logic.
- Inspected application flow.
- Located hardcoded secrets.

---

### 3. Manifest Analysis

Reviewed AndroidManifest.xml for:

- Exported components
- Dangerous permissions
- Backup configuration
- Cleartext traffic
- Metadata exposure
- Security misconfigurations

---

### 4. Hermes Bytecode Reverse Engineering

Recovered and analyzed the React Native Hermes bundle to identify:

- Hidden API routes
- Internal endpoints
- Application logic
- Administrative functions
- Embedded configuration values

---

### 5. Secret Discovery

Discovered multiple sensitive artifacts including:

- Hardcoded credentials
- JWT tokens
- API keys
- Debug values
- Internal configuration

---

### 6. Storage Analysis

Reviewed local storage implementation including:

- SharedPreferences
- Local secrets
- Sensitive cached data

---

### 7. API Enumeration

Recovered application endpoints including:

- Authentication APIs
- User profile APIs
- Banking operations
- Administrative endpoints
- Internal routes

---

### 8. Vulnerability Assessment

Identified multiple security issues including:

- Hardcoded Secrets
- Insecure Storage
- Client-side Authorization Logic
- Debug Information Leakage
- Manifest Misconfiguration
- Missing Code Obfuscation
- Cleartext Network Traffic
- Backup Enabled
- Administrative Endpoint Exposure

---

### 9. Risk Assessment

Each finding was evaluated according to:

- Severity
- Technical Impact
- Attack Surface
- Exploitability
- OWASP MASVS Mapping

---

### 10. Security Recommendations

The report provides remediation guidance covering:

- Secure credential management
- Encrypted local storage
- Code obfuscation
- Manifest hardening
- Secure transport configuration
- Input validation
- Server-side authorization
- Secure development practices

---

# Tools Used

- MobSF
- APKTool
- JADX
- Hermes Disassembler
- Android Debug Bridge (ADB)
- Linux CLI Utilities

---

# Standards & References

- OWASP Mobile Application Security Verification Standard (MASVS)
- OWASP Mobile Top 10
- CWE Classification

---

# Skills Demonstrated

- Android Reverse Engineering
- Static Application Security Testing (SAST)
- Mobile Application Security
- Android Manifest Analysis
- Smali Analysis
- Hermes Bytecode Analysis
- API Enumeration
- Secret Discovery
- Vulnerability Assessment
- Secure Code Review
- Technical Reporting

---

# Disclaimer

This assessment was performed against an intentionally vulnerable application for educational and portfolio purposes only.

---

# Full Technical Report

The complete assessment report, including detailed methodology, screenshots, technical evidence, vulnerability descriptions, and remediation recommendations, is available here:

https://github.com/KhaledElsayed1/offensive-security-labs/tree/main/Mobile/static%20analysis/apk-file/Document%203%201.pdf
