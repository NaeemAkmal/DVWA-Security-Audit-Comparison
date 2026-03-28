# 🛡️ Enterprise-Grade Vulnerability Assessment: DVWA Audit

### **Project Overview**
[cite_start]This project presents a high-level security audit of the **Damn Vulnerable Web Application (DVWA)**[cite: 4]. [cite_start]The objective was to conduct a comparative analysis between the industry-standard open-source scanner **OWASP ZAP** and the world-leading enterprise DAST solution, **Invicti Standard**[cite: 14, 15, 19, 382].

[cite_start]The audit focuses on identifying critical security gaps, aggregating multi-tool findings, and providing actionable remediation strategies to improve secure development practices[cite: 6, 23].

---

### **💻 Security Lab Environment**
[cite_start]A specialized virtualized environment was utilized to ensure safe and isolated testing[cite: 8, 12]:
* **Hypervisor:** VMware Workstation.
* **Attacker Node:** Windows 10 Pro (Hosting the Security Suite).
* [cite_start]**Target Node:** Metasploitable 2 Linux (Hosting the DVWA Instance)[cite: 4, 10].
* **Network Configuration:** Isolated Host-Only networking to prevent external exposure.

---

### **🛠️ Technical Stack: Invicti vs. OWASP ZAP**
[cite_start]This assessment highlights the difference between community-driven tools and enterprise-tier security software[cite: 19]:

#### **1. Invicti Standard (Enterprise Powerhouse)**
[cite_start]Invicti is a premium DAST solution trusted by global organizations for its precision and depth[cite: 382, 393].
* [cite_start]**Proof-Based Scanning:** Automatically verifies vulnerabilities to eliminate false positives, ensuring accuracy for critical flaws[cite: 395].
* [cite_start]**Deep Engine Analysis:** Detected out-of-date server components and encryption failures that are often overlooked by basic scanners[cite: 398, 415].
* [cite_start]**Compliance Mapping:** Provides detailed mapping against PCI DSS, OWASP Top 10, and ISO27001[cite: 422, 423].

#### **2. OWASP ZAP (Industry Standard)**
* [cite_start]Utilized for automated spidering and baseline security alerts[cite: 14, 19].
* [cite_start]Effective at identifying passive security risks and missing HTTP security headers[cite: 34].

---

### **📊 Comprehensive Technical Findings**
[cite_start]The following critical and high-risk issues were identified and validated across the target[cite: 32, 393, 401, 402]:

| Vulnerability Name | Severity | Primary Tool | Description & Impact |
| :--- | :--- | :--- | :--- |
| **Remote Code Execution (CVE-2012-1823)** | **Critical/High** | **ZAP** | [cite_start]Arbitrary OS command execution on the web server via PHP CGI misconfiguration[cite: 34, 36]. |
| **Source Code Disclosure (CVE-2012-1823)** | **Critical/High** | **ZAP** | [cite_start]Disclosure of raw PHP source code, potentially revealing credentials and logic[cite: 34, 36]. |
| **Out-of-date Apache (2.2.8)** | **Critical** | **Invicti** | [cite_start]The web server version is obsolete and contains numerous known exploits[cite: 398, 415]. |
| **Out-of-date PHP (5.2.4-2)** | **Critical** | **Invicti** | [cite_start]The PHP engine is end-of-life and subject to critical security vulnerabilities[cite: 398, 415, 186]. |
| **Cleartext Password Transmission** | **High** | **Invicti** | [cite_start]Sensitive credentials are sent over HTTP without SSL/TLS encryption[cite: 415, 420]. |
| **Absence of Anti-CSRF Tokens** | **Medium** | **ZAP** | [cite_start]Forms lack protection against Cross-Site Request Forgery (CSRF) attacks[cite: 34, 41]. |
| **Directory Browsing Enabled** | **Medium** | **Both** | [cite_start]Allows attackers to view and access sensitive directory listings[cite: 34, 118, 417]. |
| **Hidden File Found (phpinfo.php)** | **Medium** | **ZAP** | [cite_start]Exposure of detailed PHP configuration and environment information[cite: 34, 120]. |
| **Missing Content Security Policy (CSP)** | **Medium** | **Both** | [cite_start]Lack of CSP headers increases the risk of XSS and data injection attacks[cite: 34, 94, 415]. |
| **Missing Anti-Clickjacking Header** | **Medium** | **ZAP** | [cite_start]The site is vulnerable to UI redressing attacks due to missing X-Frame-Options[cite: 34, 121]. |
| **Cookie No HttpOnly Flag** | **Low** | **Both** | [cite_start]Session cookies can be accessed via JavaScript, leading to potential hijacking[cite: 34, 121, 415]. |

---

### **🚀 Actionable Remediation Roadmap**
1. [cite_start]**Critical Patching:** Update the web server (Apache) and backend engine (PHP) to current stable versions immediately[cite: 36, 101, 415].
2. [cite_start]**Implement Encryption:** Deploy SSL/TLS (HTTPS) to secure all data transmissions and protect user credentials[cite: 415].
3. [cite_start]**Security Header Deployment:** Configure mandatory headers including `Content-Security-Policy`, `X-Frame-Options: DENY`, and `X-Content-Type-Options: nosniff`[cite: 105, 121, 188].
4. [cite_start]**Session Hardening:** Enable `HttpOnly` and `Secure` flags on all cookies and implement robust Anti-CSRF tokens[cite: 76, 139, 417].
5. [cite_start]**Server Hardening:** Disable directory browsing and suppress server version information in HTTP headers[cite: 118, 187, 417].

---

### **📂 Repository Structure**
```text
├── Reports/            # Consolidated PDF & HTML Security Reports [cite: 18]
├── Evidence/           # Tool Dashboards and Technical Screenshots [cite: 5]
└── README.md           # Project Documentation [cite: 18]
