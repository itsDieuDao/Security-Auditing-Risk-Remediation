<h1>Security Auditing & Risk Remediation</h1>

 

**Objective**: Simulate an **IT security audit**, identify compliance gaps, and create a **remediation plan** to address risks in a home lab.
 <br/>


<h2>🛠 Step 1: Choose an Audit Framework </h2>  
  <br/>  
  
🔹 Select an **audit framework** that aligns with common industry regulations:  
   - <b> **CIS Controls v8** - General security best practices </b>  
   - <b> **NIST 800-53** - Government security standards </b>  
   - <b> **SOC 2 Type II** - Security, Availability, and Confidentially compliance </b>  
   - <b> **ISO 27001** - International security management standard </b>  

  
👉 For this project, we'll use **CIS Controls v8**, which is widely applicable across industries. <br/>  
📄 Download the **CIS Controls v8** [HERE](https://www.cisecurity.org/controls/v8-1) <br/>  

  
<h2>🛠 Step 2: Conduct a Security Audit </h2>  

An audit assesses **security controls** and finds **gaps** We'll review:  
✅ **Access Controls** (Who has access to what?)  
✅ **Logging & Monitoring** (Are events properly logged?)  
✅ **Vulnerability Management** (Are systems patched and updated?)  
✅ **Network Security** (Are firewalls & segmentation in place?)  

  
<h2>🔹 Step 2.1: Perform an Audit in Your Home Lab </h2>  
🔧 Windows Server: Check Security Settings    
  <br/>   
 
📌 List **User Accounts & Privileges**

    Get-LocalUser | Select Name, Enabled  
    
- Identify inactive accounts that should be removed.

📌 Check **Group Policies Applied**  

    gpresult /h C:\AuditReport.html  
  
- Review **password policies, firewall settings, and remote access rules.**

📌 Check **Event Logs for Security Issues**  

    Get-EventLog -LogName Security -Newest 10  
    
- Look for **failed login attempts** or suspicious activities.
  
  
<h3>🛠 Linux: Perform a Security Audit </h3>  
  
📌 Check **Active User Accounts**  

    cat /etc/passwd | cut -d: -f1  

- Identify **unused accounts** that should be disabled.

📌 List **Open Ports (Identify Unneccessary Services)**  

    netstat -tulnp  

- Close **uneeded ports** to reduce attack surface.
  
📌 Check **unneeded ports** to reduce attack surface.  

    sudo apt update && sudo apt list --upgradable  

- Patch any **outdated** software.

📌 Scan **System for CIS Compliance Using Lynis**  

    sudo apt install lynis -y
    sudo lynis audit system  

- Review **security hardening recommendations.**
  

  <h2>🛠 🔹 Step 2.2: Identify Security Gaps <br/>  
   
 After running audits, document security gaps.
  
  🔹 **Example Findings:**  
  
| Category | Issue Identified | Risk Level |
| -------- | ---------------- | ---------- |
| Access Control | Default administrator account active | High |
| Logging & Monitoring | No log retention policy set | Medium | 
| Patching | Linux kernel outdated | High |
| Firewall | Open SSH port exposed to internet | Critical |  

    
 <h2>🛠 Step 3: Create a Remediation Plan </h2>  

  Now that we've identified risks, lets **priortize** and **fix them.**  

   🔹 **Example Remediation Actions:**  
   
| Risk | Remediation Action | Owner | Deadline |
| ---- | ------------------ | ----- | -------- | 
| Weak Admin Account | Disable default admin account | IT Admin | ASAP | 
| No Log Retention Policy | Implement a 90-day log retention | Security Team | 1 Week | 
| Outdated Software | Apply latest security patches | SysAdmin | 1 Week | 
| Open SSH Port | Restrict SSH access to internal IPs | Network Team | ASAP | 

  

<h2>🛠 Step 4: Implement Fixes in Home Lab </h2>    
  
 <h3>🔹 Remediate Access Control Issues </h3>   

  
  **Windows: Disable Default Administrator Account**  
  
        Disable-LocalUser -Name "Administrator"  
 
✅ **Prevents unauthorized access.**
  
 **Linux Restrict SSH Access**  

      sudo nano /etc/ssh/sshd_config
    # Add or modify:
      PermitRootLogin no
      AllowUsers your_user
  </br>    
    
     sudo systemctl restart ssh  
  

✅ **Blocks SSH brute-force attacks.**  

  
<h2>🔹 Configure Log Retention </h2>  

**Windows: Enable Log Retention Policy**  

  
1. Open **Group Policy Editor (gpedit.msc)**
2. Navigate to:
   `Computer Configuration > Windows Settings > Security Settings > Event Log`
3. Set **Max Log Size** = **100MB** & **Retention Period** = **90 Days**

 **Linux: Set Log Retention to 90 Days**  

   Modify log rotation settings:  

    sudo nano /etc/logrotate.conf  

  Add or modify:  

    /var/log/auth.log {
        rotate 12
        weekly
        compress
        missingok
    }  

  ✅ **Ensures logs are kept for security investigations. **  


  
  
<h2> 🔹 Patch Vulnerabilites & Secure Firewall </h2>    

 **Windows: Apply Updates**  

    Get-WindowsUpdate -Install -AcceptAll -AutoReboot  

**Linux: Apply Updates & Restrict SSH to Internal IPs**  

    sudo apt update && sudo apt upgrade -y
    sudo ufw allow from 192.168.1.0/24 to any port 22  

 ✅ **Prevents external SSH attacks.**  


 <h2>🛠 Step 5: Verify & Report Compliance </h2>  

 🔹 **Re-Audit to Confirm Fixes**  
 After implementing fixes, rerun security checks:  

 - **Windows:**

       Get-LocalUser | Select Name, Enabled
     
 - **Linux:**

       sudo lynis audit system  

 - **Firewall CHeck:**

       sudo ufw status verbose  

  <h2> 📝 Sample Audit Remediation Report </h2>  
  
**IT Security Audit & Risk Remediation Report**  
**Date:** \[2/14/2025]  
**Framework:** CIS Controls v8  

<h3> 🔹 Summary of Audit Findings </h3>  

| Category | Issue Found | Status | 
| -------- | ----------- | ------ | 
| Access Control | Default admin account active | ✅ Disabled | 
| Logging & Monitoring | No log retention policy | ✅ Set to 90 days | 
| Patching | Outdated Linux Kernel | ✅ Patched | 
| Firewall | SSH exposed to the internet | ✅ Restricted to internal network | 

<h3> 🔹 Remaining Risks </h3>

 📌 No **multi-factor authentication (MFA)** configured  
 📌 **SIEM integration** not yet implemented  

  

<h3> 🔹 Next Steps </h3>  

   1. Implement **MFA for all admin accounts**
   2. Deploy **SIEM (Wazuh, Splunk) for centralized log monitoring**
   3. Automate compliance checks with **scripts & dashboards.**  

  


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
