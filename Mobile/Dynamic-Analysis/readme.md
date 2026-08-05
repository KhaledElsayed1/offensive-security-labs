# Combined Mobile Security Assessment (SAST & DAST)

A comprehensive Mobile Application Security Assessment demonstrating both **Static Application Security Testing (SAST)** and **Dynamic Application Security Testing (DAST)** techniques against the intentionally vulnerable **InsecureShop** Android application.

This project documents the complete assessment lifecycle, from reverse engineering and source code analysis to runtime instrumentation, network interception, local storage inspection, and remediation planning.

> **Disclaimer**
>
> This assessment was performed against an intentionally vulnerable application for educational, research, and portfolio purposes only.

---

# Objectives

The objectives of this assessment were to:

- Perform Static Application Security Testing (SAST)
- Perform Dynamic Application Security Testing (DAST)
- Analyze Android application architecture
- Inspect application runtime behavior
- Intercept and analyze network traffic
- Evaluate session management mechanisms
- Inspect local storage security
- Assess SSL/TLS validation behavior
- Correlate static findings with runtime exploitation
- Provide actionable remediation recommendations

---

# Assessment Scope

The assessment covered the following areas:

- Static Code Review
- Android Manifest Analysis
- Runtime Monitoring
- API Interception
- Authentication & Session Handling
- Local Storage Inspection
- SQLite Analysis
- SharedPreferences Analysis
- SSL/TLS Validation
- Certificate Pinning Evaluation
- Runtime Information Leakage
- Static & Dynamic Finding Correlation

---

# Assessment Workflow

## 1. Static Application Security Testing (SAST)

- APK inspection
- Manifest analysis
- Source code review
- Security configuration review
- Vulnerability identification

---

## 2. Dynamic Application Security Testing (DAST)

- Emulator configuration
- Runtime instrumentation
- Process monitoring
- Logcat analysis
- Application behavior validation

---

## 3. Network Security Assessment

- Proxy configuration
- HTTPS interception
- HTTP traffic inspection
- API request analysis
- Session token verification

---

## 4. Local Storage Assessment

- SharedPreferences inspection
- SQLite database analysis
- Cache review
- Sensitive data validation

---

## 5. Runtime Security Analysis

- Runtime logging
- Memory inspection
- Certificate validation behavior
- SSL error handling
- Debug information exposure

---

## 6. Security Correlation

Static findings were validated through dynamic analysis to determine whether identified weaknesses could be observed or confirmed during application execution.

---

# Security Findings

The assessment identified multiple security issues including:

- Insecure Network Communication
- Weak Session Management
- Cleartext Data Storage
- SSL/TLS Validation Weaknesses
- Certificate Validation Issues
- Runtime Information Disclosure
- Debug Information Exposure
- Insecure Local Storage
- Missing Secure Transport Controls
- Configuration Weaknesses

---

# Tools Used

- MobSF
- Burp Suite Professional
- Frida
- Android Debug Bridge (ADB)
- Genymotion Emulator
- Android SDK Platform Tools
- SQLite
- Logcat

---

# Skills Demonstrated

- Mobile Application Security
- Android Security Testing
- Static Analysis (SAST)
- Dynamic Analysis (DAST)
- API Security Testing
- Runtime Instrumentation
- Reverse Engineering
- Network Traffic Analysis
- Burp Suite
- Frida
- Local Storage Analysis
- Session Security Assessment
- Secure Code Review
- Technical Security Reporting

---

# Standards

- OWASP Mobile Application Security Verification Standard (MASVS)
- OWASP Mobile Top 10

---

# Repository Structure

```
Mobile/
└── dynamic analysis/
    ├── README.md
    ├── screenshots/
    └── Android_SAST_DAST_Security_Assessment.pdf
```

---

# Full Technical Report

The complete assessment report, including screenshots, technical evidence, runtime observations, identified vulnerabilities, and remediation recommendations, is available here:

**Report**

https://github.com/KhaledElsayed1/offensive-security-labs/tree/main/Mobile/dynamic%20analysis

---

# Author

**Khaled Elsayed**

GitHub:
https://github.com/KhaledElsayed1

---

## License

This repository is intended solely for educational, research, and portfolio purposes.
No attacks were performed against production systems or unauthorized targets.
