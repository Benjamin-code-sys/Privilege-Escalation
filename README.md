# Local Privilege Escalation Misconfigurations  
_A brief overview for red-team documentation_

## 🔹 Introduction
Local Privilege Escalation (LPE) refers to weaknesses that allow an attacker with limited access (e.g., standard user) to gain higher privileges such as admin or SYSTEM.  
During a red team engagement, identifying these misconfigurations helps simulate realistic attacker behaviour and demonstrates how small flaws can lead to full system compromise.

---

## 🔹 Common Types of Misconfigurations
- **Weak File/Folder Permissions**  
  Executables, scripts, or service paths that standard users can modify, enabling unauthorized changes.

- **Misconfigured Services**  
  Services running with high privileges but poorly secured configurations, allowing unintended control or abuse.

- **Credential Mismanagement**  
  Stored plaintext passwords, weak permission settings, or unattended configuration files exposing sensitive data.

- **Insecure Registry Permissions**  
  Registry keys writable by low-privileged users that affect high-privileged processes.

- **Outdated or Unpatched Software**  
  Legacy applications or OS components that contain known privilege-escalation flaws.

---

## 🔹 Why LPE Matters in Red Teaming
- **Realistic Attack Progression**  
  Attackers rarely start with admin rights—LPE mimics real-world intruder methodology.

- **Demonstrates Business Impact**  
  Shows how small configuration oversights can lead to domain-wide compromise.

- **Validates Defense & Monitoring**  
  Helps organizations test detection capabilities for privilege misuse or suspicious escalation activity.

- **Supports Post-Exploitation Objectives**  
  Gaining higher privileges enables lateral movement, credential extraction, persistence, and full environment mapping.

---

## 🔹 Conclusion
Local Privilege Escalation misconfigurations are a critical focus area in red team engagements. Identifying and reporting them strengthens organizational security, ensures better configuration practices, and highlights the importance of continuous hardening across systems.  

In this repository i'll be demostrating five diffrent ways misconfigurations can lead to escalation to _**administrators**_ and even _**System**_

