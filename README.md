# **Wazuh: The Free SIEM That Fights Like a Paid One**

As someone who's spent countless hours dissecting networks, scanning for vulnerabilities, and escalating privileges in controlled chaos, one often forgets to appreciate the other side of the equation—the defenders. While the Red Team tests the armor, the Blue Team forges it. Enter **Wazuh**, a name that resonates deeply in the open-source security monitoring landscape.

In this article, I’ll walk you through Wazuh not as a textbook definition, but as a practical, real-world defense ally I've come to appreciate—and deploy.

---

## **What is Wazuh?**

At its core, **Wazuh is an open-source security monitoring platform** that integrates **SIEM**, **XDR**, and **compliance** capabilities into one streamlined framework. It began as a fork of OSSEC but has evolved dramatically, now standing tall among commercial-grade solutions without the price tag.

Wazuh offers:

* **Intrusion Detection (HIDS)**
* **Log Data Analysis**
* **File Integrity Monitoring (FIM)**
* **Threat Intelligence Integration**
* **Vulnerability Detection**
* **Compliance Reporting (HIPAA, GDPR, PCI-DSS, etc.)**
* **Security Incident Correlation**

All from a **centralized console** that scales with your infrastructure.

---

## **Why Wazuh? A VAPT Specialist’s Perspective**

As someone who regularly performs **penetration testing**, I’ve witnessed the aftermath of successful lateral movements, unmonitored file modifications, and misconfigured agents. Wazuh, when properly configured, can detect **most of these activities in near real-time**.

Here’s why I recommend Wazuh:

### 1. **Real-Time File Integrity Monitoring (FIM)**

When I test Linux or Windows systems, one of my goals is persistence. Wazuh’s FIM detects changes to binaries, configuration files, or cron jobs—alerting defenders instantly.

> Want to monitor `.bashrc`, `/etc/passwd`, or a web directory? Wazuh does that by default.

### 2. **Built-in MITRE ATT\&CK Mapping**

Wazuh alerts are **automatically mapped to MITRE TTPs**. During a red team simulation, the blue team was able to correlate privilege escalation attempts with known ATT\&CK techniques. That was game-changing.

### 3. **Threat Intelligence Integration**

Wazuh integrates with **AlienVault OTX**, **VirusTotal**, and **MISP**. I once fed IoCs from a phishing campaign into Wazuh, and within seconds, endpoints communicating with the malicious domain lit up on the dashboard.

### 4. **Vulnerability Detection**

Wazuh parses OS packages, compares them with vulnerability databases (like NVD), and alerts if any CVEs match. If you’re running unpatched Apache or OpenSSL—Wazuh will shout about it.

---

## **Architecture Overview**

**Wazuh comprises three major components:**

* **Wazuh Agent** – Installed on monitored endpoints (Linux, Windows, macOS).
* **Wazuh Manager** – Parses logs, applies rules, and generates alerts.
* **Wazuh Dashboard (via Kibana/OpenSearch)** – Visualize logs, hunt threats, and respond.

Add **Elastic Stack** or **OpenSearch** to scale to thousands of nodes.

![Picture1](https://github.com/user-attachments/assets/cab0c065-87bc-4c89-8e7f-702268682a6d) <br/>

Image Credits:
S. Stanković, S. Gajin, and R. Petrović, "A Review of Wazuh Tool Capabilities for Detecting Attacks Based on Log Analysis," in Proc. IX Int. Conf. IcETRAN, Novi Pazar, Serbia, Jun. 6–9, 2022, pp. RTI2.6. [Online]. Available: https://www.etran.rs/2022/zbornik/ICETRAN-22_radovi/068-RTI2.6.pdf

---

## **Use Case: Detecting Reverse Shells**

While testing a corporate workstation, I deployed a Python reverse shell as a part of privilege escalation. Without endpoint monitoring, this would’ve gone unnoticed. But Wazuh, configured with **syscall monitoring** and **command audit**, instantly flagged the execution of `/bin/bash -i >& /dev/tcp/`.

Paired with **Sysmon on Windows**, it’s even more powerful—detecting PowerShell-based payloads, encoded command executions, and persistence via registry modifications.

---

## **CTF Meets SOC: Wazuh in a Simulated Environment**

In one of my internal **Capture The Flag exercises**, I set up Wazuh as the defending SIEM. As the Red Team launched DNS tunneling, Wazuh’s anomaly detection and custom rules fired. This exercise taught my team that **good alerting is only half the battle**—the other half is **tuning**.

> False positives are inevitable. But with custom rules and decoders, Wazuh can be sharpened to your environment’s heartbeat.

![Picture2](https://github.com/user-attachments/assets/1d0ecbf3-43ae-408d-8efa-abc5564914fa) <br/>

Image Credits:
S. Stanković, S. Gajin, and R. Petrović, "A Review of Wazuh Tool Capabilities for Detecting Attacks Based on Log Analysis," in Proc. IX Int. Conf. IcETRAN, Novi Pazar, Serbia, Jun. 6–9, 2022, pp. RTI2.6. [Online]. Available: https://www.etran.rs/2022/zbornik/ICETRAN-22_radovi/068-RTI2.6.pdf


---

## **Integrations & Automation**

* **Sysmon + Wazuh on Windows**
* **Suricata + Wazuh for network-level IDS**
* **YARA + Wazuh for malware detection**
* **OSQuery + Wazuh for endpoint queries**
* **ElasticSearch/OpenSearch for querying and alerting**

Pair it with **TheHive** or **Cortex** for automated case management and response.

---

## **Limitations to Watch Out For**

Nothing is perfect, and Wazuh has its share of challenges:

* **Resource Intensive** on large deployments.
* **Steep Learning Curve** for newcomers.
* **Tuning Required** — or you’ll drown in alerts.
* **Kibana/OpenSearch** dashboards require constant maintenance.

But for an open-source solution, the **benefits far outweigh the drawbacks**.

---

## **Final Thoughts: From Red to Blue**

As someone who regularly steps into Red Team shoes, I value tools that make my job harder—but also teach defenders how to think offensively. **Wazuh** does exactly that.

It's not just a monitoring solution; it’s a training ground for Blue Teamers, SOC analysts, and cybersecurity enthusiasts to **see the unseen, detect the stealthy, and respond with precision**.

> Wazuh isn't just software—it's a philosophy: monitor everything, assume compromise, and stay alert.

---
