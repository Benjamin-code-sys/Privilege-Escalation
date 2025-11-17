# 🚫 UAC Bypass via Fodhelper 

##  What Is Fodhelper?
**Fodhelper.exe** is a legitimate Windows system utility used for managing “Features on Demand.”  
It is a **trusted**, **auto-elevated** binary—meaning Windows allows it to run with elevated privileges *without prompting UAC* when launched from certain protected paths.

This trust model is where the risk begins.

---

##  How the Misconfiguration Happens
Windows relies on specific registry entries to determine how Fodhelper should behave during launch.  
If those registry paths are:

- writable by a standard user  
- consulted by Fodhelper before execution  
- and not checked by UAC  

…then an attacker with *local, low-privileged access* may influence what Fodhelper loads when it auto-elevates.

> The issue is not Fodhelper itself—it's **how Windows trusts it** and **how the registry can be misconfigured**.

---

## 🔺 Why This Can Lead to UAC Bypass
Since Fodhelper elevates **without showing a UAC prompt**, any user-controlled configuration it loads will inherit the elevated context.  
This means a normal user can indirectly trigger an elevated process *without providing admin credentials or seeing a UAC pop-up*.

This is a bypass of the UAC protection boundary, but **not** a total security break on its own.  
It relies heavily on misconfigured or weak registry permissions.

---

## Impact During Red Team Assessments
- **Demonstrates Weak UAC Configuration**  
  Shows that UAC settings, while helpful, can be bypassed if trusted apps rely on writable registry keys.

- **Shows Realistic Attacker Progression**  
  Many attackers target UAC bypasses to quietly elevate privileges without alerting the user.

- **Enables Higher-Level Actions**  
  Once bypassed, the elevated context can be used to:
  - perform system modifications  
  - access restricted files or settings  
  - prepare persistence mechanisms  
  - escalate further depending on system posture  

- **Highlights Policy Gaps**  
  Weak UAC or registry permissions often appear in environments with legacy configurations or unmanaged workstation policies.

---

## 🛡️ Defensive Mitigation
- Make sure **UAC is set to the highest enforcement level**, requiring credentials for elevation.  
- Audit and restrict **registry write permissions**, especially for keys read by auto-elevated binaries.  
- Use **application whitelisting** or endpoint monitoring to flag suspicious interactions with trusted system binaries.  
- Keep Windows updated and prune legacy configurations where possible.

---

## Summary
The Fodhelper UAC bypass isn't magic—it’s a combination of:  
- a trusted, auto-elevated Windows tool  
- registry paths that can be influenced by low-privileged users  
- and a UAC model that assumes those registry entries are secure  

In red team engagements, this misconfiguration illustrates how **small trust assumptions can open pathways to silent privilege elevation**.

