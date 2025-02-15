<h1>Security Auditing & Risk Remediation</h1>

 

**Objective**: Understand how to map security controls to compliance frameworks (e.g., NIST CSF, ISO 27001, SOC 2) and test compliance in a home lab.
 <br/>


<h2>🛠 Step 1: Choose a Compliance Framework</h2>
You can start with NIST Cybersecurity Framework (CSF) since it's widely used and publicly available.<br/>   
  <br/>  
  
🔹 Alternative Options :  
  - <b>ISO 27001 (if you want international standards)</b> 
   - <b>SOC 2 (if you're interested in auditing for service providers)</b>
   - <b>PCI-DSS (for payment security compliance)</b>

👉 For this project, we'll use NIST CSF as our baseline framework. <br/>  
📄 Download the NIST CSF document [HERE](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.04162018.pdf) <br/>  

  
<h2>🛠 Step 2: Set Up Your Home Lab </h2>
   
<h3>🔹 Install a Windows Server & Linux VM </h3>  
We'll map compliance requirements to actual security settings in a controlled environment.<br/>   
  <br/>  

   🔧 Tools & Setup:
   - <b>Windows Server 2022 (or 2019) VM</b> - For Group Policy, logging, and access control </b>
   - <b>Ubuntu/Debian VM</b> - For security configuration and compliance scanning </b>
   - <b>pfSense VM (Optional)<b/> - If you want to add firewall policies
 
📌 Install Virtual Machines (VMs)
1. Download and install VMware Worrkstation / VirtualBox
2. Set up Windows Server 2022 and Ubuntu 22.04 VMs
3. Configure a domain controller (Active Directory) on Windows Server <br/>


<h2>🛠 Step 3: Map NIST CSF Controls to Your Lab Environment</h2>
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
