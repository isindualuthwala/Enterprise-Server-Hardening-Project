# Enterprise-Server-Hardening-Project

**Module:** IE3062 - Data and Operating Systems Security
**Topic:** Secure Infrastructure Implementation (OS, Database, Big Data)

## 📖 Project Overview
This repository contains the practical implementation and documentation for a secure HR database system acting as a Junior System Administrator. The project follows a defense-in-depth approach, hardening the infrastructure from the Operating System level up to the Database application layer.

## 🛠️ Technology Stack
* **Operating System:** Oracle Linux 8.10 (Enterprise-grade RHEL compatible)
* **Database:** Oracle Database 23ai Free
* **Virtualization:** Oracle VirtualBox 
* **Tools:** SQLPlus, Bash, Fail2Ban, Firewalld, OpenSSH

## 🛡️ Key Implementations

### 1. OS Security (Oracle Linux)
Selected Oracle Linux for its enterprise optimization and RHEL compatibility
* **Kernel & Updates:** Configured `dnf-automatic` for unattended security updates
* **Network Security:**
    * Configured **Firewalld** with strict whitelisting (Ports 22, 80, 443, 1521 allowed; others denied)
    * Hardened **SSH** (Disabled root login, Key-based auth only, Max retries limited to 3).
* **Intrusion Prevention:** Installed and configured **Fail2Ban** to protect SSH against brute-force attacks.
* **Access Control:** Enforced **SELinux** in `Enforcing` mode for mandatory access control
* **Account Security:** Implemented strong password policies via `pwquality` (Min length 12, complexity class 3) and account lockout policies via `faillock`.

### 2. Database Security (Oracle 23ai)
* **Authentication:** Created a custom profile `C##STRONG_PROFILE` enforcing strict password lifetimes and locking accounts after 5 failed login attempts
* **Network Encryption:** Configured `sqlnet.ora` to force **AES256** encryption for all network traffic and enabled Valid Node Checking (IP Whitelisting).
* **Access Control (RBAC):** Implemented Role-Based Access Control separating duties between System Admins, Managers, and Executives.
* **Data Protection:**
    * **Virtual Private Database (VPD):** Implemented row-level security policies (`MGR_CUSTOMER_VPD`) to ensure Managers only see specific customer data.
    * **Data Redaction:** Masked sensitive columns (e.g., `CustomerSalary` and partial masking of `PhoneNo`).
    * **Encryption:** Applied Transparent Data Encryption (TDE) using AES256 on sensitive columns.
* **Auditing:** Enabled Unified Auditing to capture failed logins (ORA-01017) and suspicious DDL changes.

### 3. Big Data Security Analysis
Included a theoretical analysis of security challenges in Big Data environments.
* **Threat Modeling:** Analyzed SQL Injection, Ransomware, and Inference attacks
* **Mitigation Strategies:** Proposed differential privacy, input validation, and redundant infrastructure for DoS protection. 
