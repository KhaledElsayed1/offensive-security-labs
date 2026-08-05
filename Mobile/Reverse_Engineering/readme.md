## Android Reverse Engineering & Security Hardening Assessment

A comprehensive Android application security assessment demonstrating advanced **Static Application Security Testing (SAST)**, reverse engineering, application hardening evaluation, and **OWASP MASVS v2** compliance validation.

This project documents a full static security assessment of the intentionally vulnerable **Evil Bank** Android application, highlighting common security weaknesses, reverse engineering techniques, and recommended remediation strategies used in professional mobile application security assessments.

> **Disclaimer**
>
> This project was conducted in a controlled laboratory environment against an intentionally vulnerable application for educational, research, and portfolio purposes only.

---

# Project Objectives

The assessment focused on:

- Reverse engineering Android applications
- Static Application Security Testing (SAST)
- AndroidManifest.xml security auditing
- Java source code analysis
- Smali code inspection
- Resource and configuration analysis
- Code obfuscation evaluation
- Secret discovery
- Transport security validation
- Application hardening assessment
- OWASP MASVS compliance verification

---

# Assessment Scope

The assessment included:

- APK Decompilation
- AndroidManifest.xml Review
- Java Code Analysis
- Smali Analysis
- Resource File Inspection
- Network Configuration Review
- Code Obfuscation Assessment
- Secret Discovery
- Runtime Protection Verification
- Security Hardening Evaluation

---

# Assessment Methodology

The assessment followed a structured workflow consisting of five major phases.

## Phase 1 — APK Decompilation

- APKTool
- Resource extraction
- Manifest parsing
- Smali generation

---

## Phase 2 — High-Level Code Reconstruction

Using JADX to inspect:

- Application architecture
- Business logic
- Network operations
- Sensitive methods
- Internal classes

---

## Phase 3 — Automated Static Analysis

Using MobSF to obtain:

- Security score
- Manifest analysis
- Permission review
- Cryptographic fingerprints
- Binary metadata

---

## Phase 4 — Manual Security Review

Manual analysis included:

- Source code inspection
- Configuration review
- Secret discovery
- Logging analysis
- Network configuration validation

---

## Phase 5 — Binary Integrity Verification

Pattern matching across the decompiled application to identify:

- Root detection
- Emulator detection
- Anti-debugging
- Certificate pinning
- Play Integrity
- SafetyNet
- Code obfuscation
- Runtime protections

---

# Security Findings

The assessment identified multiple security weaknesses, including:

- Hardcoded Debug Credentials
- Sensitive Information Leakage
- Hardcoded API Keys
- Cleartext HTTP Communication
- Missing Certificate Pinning
- Missing Root Detection
- Missing Emulator Detection
- Missing Anti-Tampering Controls
- Lack of Secure Storage
- Missing Code Obfuscation
- Insecure Backup Configuration

---

# Tools Used

- MobSF
- APKTool
- JADX GUI
- grep
- Kali Linux
- Android SDK Platform Tools

---

# Skills Demonstrated

- Android Reverse Engineering
- Static Application Security Testing (SAST)
- Secure Code Review
- AndroidManifest Analysis
- Smali Analysis
- Secret Discovery
- Application Hardening Assessment
- Mobile Security Architecture Review
- OWASP MASVS Mapping
- Technical Security Reporting

---

# Security Standards

This assessment references:

- OWASP MASVS v2
- OWASP MASTG
- Android Security Best Practices
- Google Play Integrity Recommendations

---

# Repository Structure

```
Mobile/
└── reverse engineering/
    ├── README.md
    ├── screenshots/
    └── Android_Reverse_Engineering_and_Security_Hardening_Report.pdf
```

---

# Full Technical Report

The complete technical report, including methodology, screenshots, reverse engineering evidence, vulnerability analysis, OWASP MASVS mapping, and remediation recommendations, is available in this directory:

📄 **Android_Reverse_Engineering_and_Security_Hardening_Report.pdf**

Repository:

https://github.com/KhaledElsayed1/offensive-security-labs/tree/main/Mobile/reverse%20engineering

---

# Author

**Khaled Elsayed**

GitHub:
https://github.com/KhaledElsayed1

---

## License

This repository is intended for educational, research, and portfolio purposes only. All analysis was conducted against an intentionally vulnerable Android application in a controlled environment.
