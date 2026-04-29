# 🔐 SOC Alert Monitoring - Brute Force Detection using Splunk

## 📌 Overview
This project demonstrates a real-world SOC (Security Operations Center) use case for detecting brute force attacks on a web application using Splunk SIEM.

The lab simulates attacker behavior using Burp Suite and analyzes authentication logs to identify malicious login attempts through log correlation and alerting.

---

## 🛠️ Tools & Technologies
- Splunk Enterprise (SIEM)
- Splunk Universal Forwarder (Log Collection)
- Ubuntu Server (Web Application Hosting)
- Burp Suite (Attack Simulation)
- Apache Web Server Logs

---

## 🚨 Use Case: Brute Force Attack Detection

### 🎯 Objective
Detect multiple failed login attempts and identify brute force behavior using log correlation based on:
- Source IP
- Username
- Time window
- Failed login count

---

## 🔍 Detection Logic

Brute force activity is identified when:
- 4–10 failed attempts → Medium severity
- >10 failed attempts within 5–15 minutes → High severity

### 📊 SPL Query (Example)
```spl
index=web_logs STATUS=Failed
| stats count by src_ip, username
| where count > 3
```

---

## 📥 Log Collection

Logs were collected using Splunk Universal Forwarder from:
- Web application authentication logs (`login.log`)
- Apache access logs
- System authentication logs

Captured fields include:
- Source IP
- Username
- Timestamp
- Login status (SUCCESS / FAILED)

---

## 🧪 Attack Simulation

- Burp Suite used to perform brute force attack
- Payloads configured for username & password fields
- Multiple login attempts generated
- Logs ingested into Splunk in real-time

---

## 🚨 Alerting & Correlation

- Alerts triggered when failed attempts exceed threshold
- Correlation based on:
  - IP address
  - Username
  - Time window

### 🔔 Alert Name:
**Brute Force Login Attempt Detected**

---

## 🧑‍💻 SOC Investigation Workflow

1. Validate alert authenticity  
2. Check source IP (internal vs external)  
3. Analyze number of failed attempts  
4. Review historical login behavior  
5. Identify multiple targeted accounts  
6. Confirm brute force pattern  

---

## 🛡️ Incident Response

### Containment:
- Temporarily block attacker IP (iptables)
- Restrict access to web application

### Recovery:
- Unblock IP after validation
- Enforce password reset (if needed)

---

## 📊 Screenshots

> (Add your screenshots in /screenshots folder)

- Splunk dashboard
- Failed login logs
- Alert triggered
- Burp Suite attack simulation

---

## 📈 Key Learnings

- SIEM log correlation techniques  
- Splunk SPL query writing  
- Brute force detection strategies  
- Alert tuning & false positive reduction  
- SOC investigation workflow  
- Incident response handling  

---

## 🔮 Future Improvements

- SOAR automation for response  
- Geo-IP enrichment  
- Threat intelligence integration  
- Advanced anomaly detection  

---

## 👤 Author
Chandan G  
Aspiring SOC Analyst | SIEM | Blue Team
