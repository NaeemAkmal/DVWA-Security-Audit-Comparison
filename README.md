# 🛡️ Enterprise-Grade Vulnerability Assessment: DVWA Audit

### **Project Overview**
This project presents a high-level security audit of the **Damn Vulnerable Web Application (DVWA)**. The objective was to conduct a comparative analysis between the industry-standard open-source scanner **OWASP ZAP** and the world-leading enterprise DAST solution, **Invicti Standard**. 

The audit focuses on identifying critical security gaps, aggregating multi-tool findings, and providing actionable remediation strategies to improve secure development practices.

---

### **💻 Security Lab Environment**
A specialized virtualized environment was utilized to ensure safe and isolated testing:
* **Hypervisor:** VMware Workstation
* **Attacker Node:** Windows 10 Pro (Hosting the Security Suite)
* **Target Node:** Metasploitable 2 Linux (Hosting the DVWA Instance)
* **Network Configuration:** Isolated Host-Only networking to prevent external exposure

---

### **🛠️ Technical Stack: Invicti vs. OWASP ZAP**
This assessment highlights the difference between community-driven tools and enterprise-tier security software:

#### **1. Invicti Standard (Enterprise Powerhouse)**
Invicti is a premium DAST solution trusted by global organizations for its precision and depth.
* **Proof-Based Scanning:** Automatically verifies vulnerabilities to eliminate false positives, ensuring 100% accuracy for critical flaws.
* **Advanced Engine Analysis:** Detected deep-seated issues such as outdated server-side components and encryption failures often overlooked by basic scanners.
* **Compliance Mapping:** Provides detailed mapping against PCI DSS, OWASP Top 10, and ISO27001.

#### **2. OWASP ZAP (Industry Standard)**
* Utilized for automated spidering and baseline security alerts.
* Highly effective at identifying passive security risks and missing HTTP security headers.

---

### **📊 Comprehensive Technical Findings**
The following critical and high-risk issues were identified and validated across the target:

| Vulnerability Name | Severity | Primary Tool | Description & Impact |
| :--- | :--- | :--- | :--- |
| **Remote Code Execution (CVE-2012-1823)** | **Critical** | **ZAP** | Arbitrary OS command execution on the web server via PHP CGI misconfiguration. |
| **Source Code Disclosure (CVE-2012-1823)** | **Critical** | **ZAP** | Disclosure of raw PHP source code, potentially revealing credentials and logic. |
| **Out-of-date Apache (2.2.8)** | **Critical** | **Invicti** | The web server version is obsolete and contains numerous known exploits. |
| **Out-of-date PHP (5.2.4-2)** | **Critical** | **Invicti** | The PHP engine is end-of-life and subject to critical security vulnerabilities. |
| **Cleartext Password Transmission** | **High** | **Invicti** | Sensitive credentials are sent over HTTP without SSL/TLS encryption. |
| **Absence of Anti-CSRF Tokens** | **Medium** | **ZAP** | Forms lack protection against Cross-Site Request Forgery (CSRF) attacks. |
| **Directory Browsing Enabled** | **Medium** | **Both** | Allows attackers to view and access sensitive directory listings. |
| **Hidden File Found (phpinfo.php)** | **Medium** | **ZAP** | Exposure of detailed PHP configuration and environment information. |
| **Missing Content Security Policy (CSP)** | **Medium** | **Both** | Lack of CSP headers increases the risk of XSS and data injection. |
| **Missing Anti-Clickjacking Header** | **Medium** | **ZAP** | Vulnerable to UI redressing attacks due to missing X-Frame-Options. |
| **Cookie No HttpOnly Flag** | **Low** | **Both** | Session cookies can be accessed via JavaScript, leading to hijacking. |

---
![App Screenshot](Screenshot%202026-03-28%20064148.png)

### **🚀 Actionable Remediation Roadmap**
1. **Critical Patching:** Update web server (Apache) and backend engine (PHP) to current stable versions immediately.
2. **Implement Encryption:** Deploy SSL/TLS (HTTPS) to secure all data transmissions and protect user credentials.
3. **Header Hardening:** Configure mandatory headers including `Content-Security-Policy`, `X-Frame-Options: DENY`, and `X-Content-Type-Options: nosniff`.
4. **Session Management:** Enforce `HttpOnly` and `Secure` flags on all cookies and implement robust Anti-CSRF tokens.

---

### **📂 Repository Structure**
```text
├── Reports/            # Final PDF & HTML Security Reports
├── Evidence/           # Dashboard Screenshots & Folder Proofs
└── README.md           # Project Documentation
