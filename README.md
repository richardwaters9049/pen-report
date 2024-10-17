# SecureCorp Web Application

## 🔒 Penetration Testing Report

### 1. Executive Summary

**Target**: SecureCorp Web Application ([https://app.securecorp.com](https://app.securecorp.com/))  
**Assessment Date**: 09/08/2024  
**Report Date**: 09/08/2024

### Assessment Overview:

The penetration test of SecureCorp's web application uncovered several critical vulnerabilities that malicious actors could exploit to gain unauthorised access to sensitive data and compromise system security. Key findings include:

- 🔑 **Directory Traversal Vulnerability** in Nginx
- 💻 **Reflected Cross-Site Scripting (XSS)** flaw
- 📂 **Open Directories**
- ⬆️ **Weak Configuration Settings** allowing SSH access and privilege escalation

These vulnerabilities pose a significant risk to the confidentiality, integrity, and availability of the systems involved. Immediate action is required to mitigate these risks effectively.

---

### 2. Key Findings

| **Vulnerability**                              | **Description**                                                                    | **Impact** | **Remediation**                                                                                         |
| ---------------------------------------------- | ---------------------------------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------- |
| **Nginx Directory Traversal (CVE-2021-23017)** | Unauthorized access to sensitive files like `/etc/passwd` and configuration files. | High       | Update Nginx to version 1.21.3 or later. Implement access controls.                                     |
| **Reflected XSS**                              | Possible injection of malicious scripts to steal session cookies.                  | High       | Sanitize user inputs and implement Content Security Policy (CSP) headers.                               |
| **Open Directory**                             | Sensitive internal files exposed without authentication.                           | Medium     | Disable directory indexing and restrict access to sensitive directories.                                |
| **Privilege Escalation**                       | Weak sudo permissions allowed escalation to root access via SSH.                   | Critical   | Enforce the principle of least privilege and secure SSH access using multi-factor authentication (MFA). |

---

### 3. Scope of Engagement

**Scope**:

- **Target**: SecureCorp Web Application ([https://app.securecorp.com](https://app.securecorp.com/))
- **IP Range**: 192.168.1.0/24 (Internal Network)
- **In-Scope Services**: Web application, SSH, underlying infrastructure
- **Out-of-Scope**: Social engineering and physical security tests were excluded from this engagement.

---

### 4. Objective

The objective of this penetration test was to assess the security posture of SecureCorp's web application and underlying infrastructure by identifying vulnerabilities and evaluating the potential impact of those vulnerabilities if exploited. This assessment aimed to provide actionable recommendations for enhancing the security of SecureCorp’s assets.

---

### 5. Methodology

The penetration test followed a structured methodology comprising five phases:

1. **Reconnaissance**: Information gathering through open-source intelligence (OSINT), DNS enumeration, and subdomain discovery.
2. **Scanning**: Network and web application scanning using tools like Nmap and Nikto to identify open ports, services, and vulnerabilities.
3. **Exploitation**: Exploiting identified vulnerabilities, including directory traversal (Nginx), XSS, and open directories.
4. **Post-Exploitation**: Evaluating the full impact of the vulnerabilities by accessing sensitive files, escalating privileges, and exploring lateral movement.
5. **Reporting**: Documenting findings and providing remediation recommendations.

---

### 6. Tools Used

- 🔍 **Nmap**: Port scanning and service detection
- 🕵️ **Nikto**: Web vulnerability scanning
- 🛡️ **OWASP ZAP**: Web application testing
- 🔑 **SSH**: Privilege escalation attempts

---

### 7. Detailed Findings

#### A. Nginx Directory Traversal (CVE-2021-23017)

- **Description**: A directory traversal vulnerability was found in the Nginx web server (version 1.18.0), allowing unauthorised access to sensitive files outside the web root.
- **Exploitation**: Accessed files like `/etc/passwd` and the `.env` file containing database credentials.
- **Impact**: High - Could compromise system integrity and escalate privileges.
- **Remediation**: Update Nginx to a patched version (1.21.3 or later). Implement access controls to prevent unauthorised file access.

#### B. Reflected Cross-Site Scripting (XSS)

- **Description**: The search parameter was vulnerable to reflected XSS, allowing attackers to inject malicious JavaScript into the browser.
- **Exploitation**: Crafted a malicious URL that injected JavaScript to steal session cookies.
- **Impact**: High - Can be used to steal user credentials or perform unauthorised actions.
- **Remediation**: Sanitize and validate all user input before rendering it in the browser. Implement Content Security Policy (CSP) headers to mitigate XSS attacks.

#### C. Open Directory Access

- **Description**: The `/uploads/` directory was accessible without authentication, exposing sensitive internal files.
- **Exploitation**: Browsed the directory and found internal documents, including a backup configuration file.
- **Impact**: Medium - Exposed files could lead to further compromise or data theft.
- **Remediation**: Disable directory indexing and restrict access to sensitive directories through proper configuration.

#### D. Privilege Escalation via SSH

- **Description**: Credentials found in the `.env` file were used to log into the server via SSH. Weak sudo permissions allowed privilege escalation to root.
- **Exploitation**: Logged into the server using the discovered credentials and escalated to root using sudo misconfigurations.
- **Impact**: Critical - Full system control could be obtained, leading to a complete compromise.
- **Remediation**: Enforce the principle of least privilege for all users. Review and restrict sudo privileges. Secure SSH access using multi-factor authentication (MFA).

---

### 8. Recommendations

1. 🔄 **Update Nginx**: Upgrade to version 1.21.3 or later to fix the directory traversal vulnerability (CVE-2021-23017).
2. 🛡️ **Implement XSS Mitigations**: Sanitize user inputs and deploy Content Security Policy (CSP) headers to prevent XSS attacks.
3. 🚫 **Restrict Directory Access**: Disable directory indexing for the `/uploads/` folder and apply proper access controls.
4. 🔑 **Secure SSH and Review Sudo Permissions**: Enforce strict sudo policies, implement multi-factor authentication (MFA) for SSH, and regularly audit access privileges.
5. 🔍 **Review Access Control Lists (ACLs)**: Ensure sensitive files are protected with the appropriate permissions and not exposed through publicly accessible directories.

---

### 9. Conclusion

The penetration test of SecureCorp's web application revealed multiple critical vulnerabilities that pose a serious risk to the security of its systems and data. The successful exploitation of these vulnerabilities could lead to full system compromise, data theft, and unauthorised access to internal systems. It is strongly recommended that SecureCorp address these issues immediately, prioritising critical vulnerabilities such as the Nginx directory traversal, privilege escalation, and XSS.

---

### 10. Relationship to Cybersecurity

This report underscores the importance of proactive cybersecurity measures in today’s digital landscape. Vulnerabilities in web applications can lead to severe consequences, including financial losses, reputational damage, and legal ramifications. By conducting regular penetration tests, organisations can identify weaknesses before malicious actors exploit them.

The findings and recommendations in this report provide a roadmap for SecureCorp to enhance its security posture, ensuring the confidentiality, integrity, and availability of sensitive data. Investing in security measures and fostering a culture of security awareness among employees is vital for maintaining a robust cybersecurity framework.
