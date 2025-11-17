## 🔹 Unquoted Service Path as a Privilege Escalation Vector

An **Unquoted Service Path** occurs when a Windows service is configured with a file path that contains spaces **but is not wrapped in quotes**.  
Example (conceptual):  
`C:\Program Files\Example App\Service.exe`  
If this path is left unquoted, Windows may misinterpret where the executable begins and ends when launching the service.

---

### 🔸 Why This Is a Security Risk
When Windows tries to start a service with an `unquoted path`, it checks multiple possible file locations.  
If any folder along that path is writable by a low-privileged user, they may place a malicious executable with a matching name in one of those interpreted locations.  
When the service (running as SYSTEM or Administrator) starts, Windows may accidentally run the malicious file instead of the legitimate one.  
This because when windows is trying to find the service binary and encouters spaces it'll execute the first letter as an exe and assume the rest are its parameters. It's flow is as described below  
<img src="https://imgur.com/p7QtcWI.png" height="65%" width="75%" alt="unquoted services Steps"/>

---

### 🔸 Impact During Red Team Engagements
- **Privilege Escalation**: A normal user could potentially execute code with SYSTEM-level privileges.
- **Persistence Opportunity**: Misconfigured paths can be abused to maintain long-term foothold.
- **Detection & Hardening Insight**: Highlights gaps in service configuration and file-system permissions that defenders often overlook.

---

### 🔸 Defensive Mitigation
- Ensure **all service paths containing spaces are enclosed in quotes**.
- Harden file and folder permissions so low-privileged users cannot write to service directories.
- Review services regularly with configuration auditing tools.

