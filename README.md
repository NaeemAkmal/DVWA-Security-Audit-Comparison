# Comparative Vulnerability Assessment: DVWA 🛡️

### **Project Overview**
This project demonstrates a comprehensive, comparative vulnerability assessment of the **Damn Vulnerable Web Application (DVWA)**. By utilizing both an open-source tool (**OWASP ZAP**) and an enterprise-grade scanner (**Invicti Standard**), I performed a systematic security audit to identify, verify, and document common web application risks.
---
### **💻 Lab Environment**
The assessment was conducted in a controlled virtual environment to ensure safety and isolation:
* **Hypervisor:** VMware Workstation
* **Attacker Machine:** Windows 10 VM (Hosting Invicti & OWASP ZAP)
* **Target Machine:** Metasploitable 2 Linux (Hosting DVWA)
* **Target URL:** `http://150.1.7.104/dvwa`

---

### **🛠️ Tools & Methodology**
The methodology followed a standard DAST (Dynamic Application Security Testing) workflow:
1.  **OWASP ZAP (Primary Tool):** Used for automated spidering and identifying passive security flaws and header misconfigurations.
2.  **Invicti Standard (Alternative Tool):** Used for deep-active scanning and proof-based vulnerability detection for complex injection points.
3.  **Aggregation:** Duplicate findings were filtered to provide a consolidated and prioritized view of the security posture.

---

### **📊 Aggregated Technical Findings**
Findings were aggregated and sorted by CVSS severity and potential business impact:

| Vulnerability | Severity | Detected By | Impact |
| :--- | :--- | :--- | :--- |
| **Out-of-date Apache/PHP** | **Critical** | Invicti | High risk of exploitation via known CVEs leading to system compromise. |
| **Password over HTTP** | **High** | Invicti | Login credentials transmitted in plain text, vulnerable to sniffing. |
| **Cloud Metadata Disclosure** | **High** | ZAP | Potential leakage of sensitive infrastructure internal data. |
| **Missing Anti-CSRF Tokens** | **Medium** | ZAP | Vulnerable to unauthorized state-changing actions via CSRF. |
| **Information Disclosure** | **Low** | Both | Reveals server banners and software versions to attackers. |

---

### **📸 Evidence**
*(Note: Visual evidence is stored in the `/Evidence` directory of this repository)*

1.  **Invicti Scan Dashboard:** Displays the risk distribution and overall security score.
2.  **Report Artifacts:** Evidence of the final PDF/HTML reports generated during the assessment.

---

### **🚀 Actionable Remediation**
* **System Patching:** Update web server components (Apache and PHP) to current stable versions.
* **Encryption:** Deploy SSL/TLS certificates to enforce HTTPS for all sensitive directories.
* **Header Hardening:** Implement security headers like `X-Frame-Options` and `X-Content-Type-Options`.
* **Session Security:** Enforce `HttpOnly` and `Secure` flags on session cookies and implement Anti-CSRF tokens.

---

### **📂 Repository Structure**
```text
├── Reports/            # Final assessment reports (PDF/HTML)
├── Evidence/           # Tool dashboards and folder screenshots
└── README.md           # Project documentation
