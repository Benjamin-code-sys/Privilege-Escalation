#  AlwaysInstallElevated — High-Level Explanation

##  What Is “AlwaysInstallElevated”?
**AlwaysInstallElevated** is a Windows Installer (MSI) policy that controls how installation packages are executed.  
When this policy is incorrectly enabled, Windows allows **any** MSI package launched by a standard user to run **with full administrative privileges**.

This setting exists for convenience in enterprise environments—but when misconfigured, it becomes a serious privilege-escalation risk.

---

## How the Misconfiguration Works
Windows uses two policy keys (one in the machine hive, one in the user hive) to determine whether MSI installers should auto-elevate:

- `Per-User` policy  
- `Per-Machine` policy  

If **both** of these are set to allow elevation, any MSI executed—regardless of who runs it—will be installed as **Administrator**.

The problem appears when:
- An organization enables these policies for deployment convenience  
- They forget to disable them  
- Standard users retain the ability to trigger elevated MSI operations  

This breaks the normal UAC and privilege boundaries.

---

## 🔺 Why This Allows Privilege Escalation
An MSI file can contain:
- application files  
- service definitions  
- registry changes  
- system modifications  

All of these actions run with whatever privilege the installer is granted.  
So if MSI installations auto-elevate, even a low-privileged user can run an installer that performs **administrator-level actions** without providing credentials.

⇒ &nbsp;&nbsp;To check whether or not AlwaysInstallElevated priv is available on a computer use the command below in the command-line
```cmd
      ◇ Get-ItemProperty -Path “HKLM:\Software\Policies\Microsoft\Windows\Installer” -Name AlwaysInstallElevated
```
```cmd
      ◇ Get-ItemProperty -Path “HKCU:\Software\Policies\Microsoft\Windows\Installer” -Name AlwaysInstallElevated 
```
This effectively hands out elevation through a misconfigured policy.

---

##  Impact in Red Team Engagements
- **Clear Privilege Escalation Vector**  
  Demonstrates how a simple policy oversight can give a basic user full administrative impact.

- **Highlights Weak Deployment Practices**  
  Shows where IT convenience has overridden security least-privilege principles.

- **Useful for Demonstrating System Risk**  
  Helps organizations understand how mismanagement of installer policies can lead to complete workstation compromise.

- **Supports Post-Exploitation Objectives**  
  Once elevated, red-teamers can validate how system controls respond to unauthorized administrative activity.

---

## 🛡️ Defensive Mitigation
- Ensure **AlwaysInstallElevated** is disabled in both policy hives.  
- Restrict software installation to trusted management systems.  
- Use application control (AppLocker, WDAC) to prevent unauthorized installers from running.  
- Audit group policies regularly, especially in hybrid or legacy environments.

---

##  Summary
The AlwaysInstallElevated misconfiguration is a classic example of **privilege escalation caused by convenience-driven policy choices**.  
When enabled on both policy hives, it allows any MSI—legitimate or not—to run as administrator, breaking core Windows security boundaries.  
During red team assessments, it’s a powerful illustration of how small policy decisions can create large security risks.

