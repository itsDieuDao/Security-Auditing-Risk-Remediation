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
  
NIST CSF has five core functions:
  
1. Identify 🏷️ – Asset management, risk assessment
2. Protect 🔒 – Access control, endpoint security
3. Detect 👀 – Logging, SIEM, monitoring
4. Respond 🚨 – Incident response plans
5. Recover 🔄 – Backup, disaster recovery
  
🔹 Example Mapping:  
| NIST Function | Control Example | Implementation in Lab |
| ------------- | --------------- | --------------------- |
| Identify      | Asset Inventory | List devices on the network using `nmap` or `PowerShell` `Get-ADComputer` |
| Protect       | Access Control  | Set up Active Directory user roles & GPO for password polices | 
| Detect        | Security Logging | Install **Splunk** or **Wazuh** to collect logs from Windows/Linux |
| Respond       | Incident Response | Simulate a **failed login attack** and analyze logs |
| Recover       | Backup & Restore | Set up **Windows Backup & Linux snapshots** |  

✅ Goal: Implement at least one security control for each NIST function in your home lab.  

<h2>🛠 Step 4: Implement Compliance Controls <br/>  
   
🔹 Windows Server Hardening (Protect & Detect) </h2>  
  
  🔧 Tasks:  
  1. Enable Password Policies
      - Open **Group Policy Editor (gpedit.msc)**
      - Navigate to `Computer Configuration > Windows Settings > Security Settings > Account Policies > Password Policy`
      - Set **Minimum Password Length** = **12**
      - Enable **Account Lockout Policy** (3 failed attempts)
  2. **Enable Windows Logging (SIEM Integration)**
      - Open **Local Security Policy (secpol.msc)**
      - Go to `Audit Policy > Audit Logon Events` → Enable **Success & Failure**
      - Install **Splunk** or **Wazuh** to collect logs

  
 <h2>🔹 Linux Hardening (Protect & Detect)</h2>  
  
  🔧 Tasks:  
  1. **Run a Compliance Scan (NIST, CIS Benchmarks)**
  
         sudo apt install lynis -y
         sudo lynis audit system  
  - This will generate a **security report** based on NIST controls.
  
  2. **Set Up Basic Firewall Rules (UFW)**

         sudo ufw enable
         sudo ufw allow OpenSSH
         sudo ufw allow 443/tcp
         sudo ufw status verbose
  - This ensures only secure traffic is allowed.  

<h2>🛠 Step 5: Compliance Validation & Reporting  <br/>  
     
🔹 Generate a Compliance Report  </h2>  
  
 1. **Windows: Check compliance settings**  
  
        Get-GPOReport -All -ReportType HTML -Path C:\GPO_Report.html
    - This exports a **Group Policy** compliance report.
  
2. *Linux: Review Lynis Report**

       cat /var/log/lynis-report.dat
    - Look for **security misconfigurations**

3. **Analyze Security Logs with Splunk/Wazuh**
    - If you set up **Splunk**, create a **dashboard** to track compliance events.

<h2>🛠 Step 6: Write a Compliance Summary Report</h2>  

🎯 Your Deliverable: A **1-Page Compliance Report** summarizing:  

✅ Controls Implemented  
✅ Findings from Compliance Tools  
✅ Areas for Improvement  
✅ Next Steps  

<h3> 📄 Example Summary: </h3>  

**Security Compliance Report - NIST CSF Implementation in Home Lab**  
**Date:** \[Your Date]  
**Compliance Framework:** NIST Cybersecurity Framework (CSF) 

<h3> 🔹 Summary of Controls Implemented </h3>  

✅ Access Control (Windows & Linux GPOs) → PROTECT  
✅ Security Logging Enabled (Splunk/Wazuh) → DETECT  
✅ Firewall Rules (UFW, pfSense) → PROTECT  
✅ Audit Logs Reviewed → DETECT & RESPOND  

<h3> 🔹 Findings </h3>  

📌 **Windows Server Compliance Scan**: Passed 8/10 controls (Weak password policy detected)  
📌 **Linux Security Audit (Lynis)**: Hardening score 85/100 (Need SSH restriction improvement)  
📌 **Splunk Logs**: Detected 3 failed login attempts (Possible brute force)  
  
<h3> 🔹 Areas for Improvement </h3>  

  - Enforce **MFA** for **Windows Login**  
  - Implement **automatic remidiation scripts** for failed login detection

<h3> 🔹 Next Steps </h3>  

   1. Set up **Automated Compliance Monitoring** (e.g., Wazuh SIEM rules)
   2. Perform **Continuous Auditing** (Scheduled CIS Benchmark scans)

  


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
