# 🛡️ WiCyS Target Defense Challenge 2025 – Complete Writeups

<div align="center">

![CTF Badge](https://img.shields.io/badge/CTF-WiCyS%202025-purple?style=for-the-badge&logo=security)
![Challenges Solved](https://img.shields.io/badge/Challenges%20Solved-11%2F12-brightgreen?style=for-the-badge)
![Ranking](https://img.shields.io/badge/Rank-25%2F896-gold?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Tier%202%20Qualified-blue?style=for-the-badge)

**My first-ever CTF experience that qualified me for Tier 2 competition**

[View Challenges](#-challenges) • [Key Learnings](#-key-learnings) • [Tools Used](#-tools-and-techniques)

</div>

---

## 🎯 Achievement Summary

This repository documents my complete journey through the **WiCyS Target Defense Challenge 2025 Tier 1**, where I achieved:

- 🏆 **11/12 challenges solved** within one month
- 📊 **25th place** out of 896 participants   
- 🚀 **Qualified for Tier 2** competition (August 21st, 2025)
- 🌟 **First-ever CTF experience** 

### 💡 Most Memorable Challenge
**D12 – Final Boss**: SD card forensic analysis involving embedded device investigation and Linux filesystem analysis.

---

## 🔍 Challenge Categories

<table>
<tr>
<td width="50%">

### 📧 **Email & Communication**
- D1: Mystery Mail
- D2: Not-so-Simple Mail Protocol  
- D3: Ransom Wrangler

### 🌐 **Network & Traffic Analysis**
- D5: Ahoy, PCAP 'n
- D6: Smuggled Away!
- D7: Endpoints and Exfiltration

</td>
<td width="50%">

### 💻 **System & Forensics**
- D8: Shadow Commit
- D9: Logging for Truth
- D10: Backup Break-in
- D11: Semi-Final Boss
- D12: Final Boss

### ❓ **Unsolved**
- D4: Trout of Office *(walkthrough included)*

</td>
</tr>
</table>

---

## 📚 Challenges

### 📨 D1 – Mystery Mail
> **Email Header Analysis | IP Attribution**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

As a member of Personalyze.io's Cybersecurity team, investigate an extortion email threatening to release stolen company data within 48 hours. Analyze email headers to determine the sender's original IP address.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Notepad, Email Header Analysis

**Methodology**:
1. Opened `.eml` file in raw text format
2. Systematically analyzed email headers
3. Traced originating IP through header chain
4. Correlated IP with sender domain

**Key Finding**: Originating IP `252.44.98.29` associated with `sgreen123@gwagm.co`

![Email Analysis](https://github.com/user-attachments/assets/34c2d07f-09a6-47dc-a8ef-336cc04c7552)
</details>

**🎓 Key Learnings**:
- Email header forensics fundamentals
- IP attribution techniques
- Importance of systematic evidence examination

---

### 📧 D2 – Not-so-Simple Mail Protocol  
> **SMTP Log Analysis | Domain Spoofing Detection**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Continue investigating the threat actor by analyzing SMTP logs in the Insightful Horizon dashboard to uncover evidence of earlier extortion attempts.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Insightful Horizon Dashboard, Log Filtering

**Methodology**:
1. Applied strategic log filtering using known domains
2. Identified domain variations and typosquatting
3. Discovered modified domain: `tgwanagm.co`
4. Located earlier threat: `tharris456@tgwanagm.co`

**Key Finding**: Subject line "*Warning: We have acquired sensitive data*"

![SMTP Logs](https://github.com/user-attachments/assets/189a8587-0a19-431b-a1f6-24337304215e)
</details>

**🎓 Key Learnings**:
- Advanced log filtering strategies
- Domain spoofing detection techniques
- Threat actor operational patterns

---

### 💰 D3 – Ransom Wrangler
> **Social Engineering | Negotiation Tactics**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Negotiate with the threat actor to reduce their Bitcoin ransom demand below 30 BTC while extending the payment deadline.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Social Engineering Principles, Negotiation Psychology

**Methodology**:
1. Applied psychological negotiation tactics
2. Focused on mutual benefit (faster payment vs. lower amount)
3. Successfully reduced ransom to **25 BTC**
4. Secured deadline extension

**Flag Extracted**: `CTF-RAN-FA5123FF: CTF-DEA-E86ED89E`

![Negotiation Process](https://github.com/user-attachments/assets/2239dea3-aaad-45dc-8bf9-5ad23fcbbb9f)
</details>

**🎓 Key Learnings**:
- Social engineering in cybersecurity context
- Negotiation psychology and tactics
- Crisis communication strategies

---

### 🎣 D4 – Trout of Office *(Unsolved - Walkthrough Included)*
> **Complex Log Correlation | Data Reconstruction**

<details>
<summary><strong>❗ Challenge Analysis</strong></summary>

While I didn't solve this during the competition, I've documented the complete solution methodology for future reference.

**Challenge Complexity**: Multi-layered log correlation with themed data mapping
- **zekes-logs-***: Fish-themed data categories (salmon=first names, trout=last names, etc.)
- **http-logs**: Application traffic analysis
- **Pivot Technique**: User-Agent filtering for non-automated requests

</details>

<details>
<summary><strong>📝 Complete Walkthrough</strong></summary>

#### Data Categories Mapping
| Fish Type | Data Type | Weight Range |
|-----------|-----------|--------------|
| Salmon | First Names | 7000-8000g |
| Trout | Last Names | 7000-8000g |
| Cod | Street Addresses | - |
| Mackerel | Cities | - |
| Halibut | States | - |
| Walleye | Zip Codes | - |
| Snapper | Credit Card (last 4) | - |
| Tuna | Noise Data (ignore) | - |

#### Solution Process
1. **Name Extraction**: Search with wildcard prefixes, filter by weight ranges
2. **HTTP Log Pivot**: Filter requests without User-Agent headers
3. **Data Assembly**: Use UUID-like IDs in API endpoints
4. **Final Reconstruction**: Combine all data points through API calls

```bash
# Example API call structure
curl -X GET "https://target-flask.chals.io/apps_per-SAPSOFT/p/[FIRST_NAME_ID]/[LAST_NAME_ID]"
```
</details>

**🎓 Key Learnings**:
- Complex multi-source data correlation
- API endpoint reconstruction techniques
- Importance of systematic approach to complex challenges

---

### 🌐 D5 – Ahoy, PCAP 'n
> **Network Traffic Analysis | DNS Tunneling Detection**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Investigate how a threat actor is exfiltrating sensitive company data by analyzing network traffic. Identify the compromised machine's hostname and the Command & Control (C2) server IP.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Wireshark, DNS Analysis, Traffic Filtering

**Methodology**:
1. Applied DNS traffic filters in Wireshark
2. Identified suspicious domain query patterns
3. Discovered DNS tunneling indicators
4. Traced communication flow: `10.75.34.13 → 251.91.13.37`

**Key Findings**:
- Compromised host: **bvlik**
- C2 IP: **251.91.13.37**
- Attack vector: DNS tunneling

![Network Analysis](https://github.com/user-attachments/assets/f88df4d6-cbf1-4dfd-afa8-65049983ca2c)
</details>

**🎓 Key Learnings**:
- DNS tunneling detection techniques
- Network traffic pattern analysis
- Wireshark advanced filtering

---

### 📡 D6 – Smuggled Away!
> **Data Exfiltration | Encoding/Decoding**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Extract stolen data (credit card details, personal information) hidden within DNS queries using encoding techniques.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Wireshark, Tshark, PowerShell, CyberChef

**Methodology**:
1. Filtered suspicious DNS queries using Wireshark
2. Extracted subdomains using Tshark command-line tool
3. Applied PowerShell regex for data cleaning
4. Decoded Base32 + Gunzip in CyberChef

**Tshark Command**:
```powershell
& "C:\Program Files\Wireshark\tshark.exe" -r "C:Desktop\pirates.pcap" -Y "ip.dst == 251.91.13.37 && dns.qry.name" -T fields -e dns.qry.name | Where-Object { ($_ -split '\.')[0] -match '^[a-zA-Z0-9]{5,}$' } | ForEach-Object { ($_ -split '\.')[0] }
```

**Extracted Data**: Complete PII including name, address, phone, email, credit card details

![Data Extraction](https://github.com/user-attachments/assets/6b887c23-ddba-49a9-a168-4c69ba611d43)
</details>

**🎓 Key Learnings**:
- DNS data exfiltration techniques  
- Base32 encoding/decoding
- Command-line forensics with Tshark
- Importance of automated extraction over manual methods

---

### 🖥️ D7 – Endpoints and Exfiltration
> **Endpoint Forensics | Process Analysis**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Identify the user, process, and software responsible for data exfiltration using system telemetry data.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: lsof, ps, history analysis

**Methodology**:
1. Correlated network connections with known C2 IP
2. Cross-referenced active processes
3. Analyzed command history for obfuscated tools
4. Identified responsible user and process

</details>

**🎓 Key Learnings**:
- Endpoint telemetry correlation
- Process forensics techniques
- Command history analysis for threat hunting

---

### 🔎 D8 – Shadow Commit  
> **Git Forensics | Supply Chain Security**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Analyze Git repository history to identify a malicious commit that introduced a hardcoded malicious IP address.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Git CLI, Repository Analysis

**Methodology**:
1. Used `git log` for commit history review
2. Applied `git diff` for change analysis
3. Identified commit with suspicious IP injection
4. Extracted commit hash and malicious IPv4

</details>

**🎓 Key Learnings**:
- Git forensics for supply chain attacks
- Repository history analysis
- Developer tool security implications

---

### 📜 D9 – Logging for Truth
> **Attribution Analysis | Audit Log Investigation**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Determine whether developer Erik was truly responsible for a suspicious commit or if he was framed by analyzing audit logs.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Insightful Horizon Dashboard, Audit Log Analysis

**Methodology**:
1. Filtered 6 months of audit logs
2. Cross-referenced commit timestamps with user activity
3. Identified IP address mismatches
4. Proved Erik's innocence through location data

</details>

**🎓 Key Learnings**:
- Importance of audit trails in attribution
- Git commit spoofing techniques
- Digital forensics investigation methodology

---

### 💾 D10 – Backup Break-in
> **Credential Discovery | Archive Analysis**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Locate leaked credentials belonging to the Git committer within backup server files.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Archive Extraction, Text Search, File Analysis

**Methodology**:
1. Extracted `.tar.gz` backup archive
2. Performed systematic plaintext searches
3. Located configuration files with embedded credentials
4. Found password beginning with `wicys`

</details>

**🎓 Key Learnings**:
- Backup server security risks
- Credential exposure in configuration files
- Systematic evidence search techniques

---

### 🗝️ D11 – Semi-Final Boss
> **Windows Registry Forensics | Persistence Analysis**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Analyze a Windows Registry hive to identify persistence mechanisms on a supposedly "clean" host.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Registry Explorer, Windows Forensics

**Methodology**:
1. Loaded Registry hive safely in specialized tool
2. Investigated common persistence locations:
   - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`
   - Services keys
   - Winlogon keys
3. Found suspicious persistence key with non-native executable

</details>

**🎓 Key Learnings**:
- Windows Registry forensics
- Persistence mechanism identification  
- Importance of specialized forensic tools

---

### 🎮 D12 – Final Boss  
> **Embedded Device Forensics | Linux Filesystem Analysis**

<details>
<summary><strong>🎯 Challenge Brief</strong></summary>

Investigate a forensic image of an SD card connected to a TinyPilot device suspected of insider threat activity.
</details>

<details>
<summary><strong>🔧 Solution Approach</strong></summary>

**Tools Used**: Linux VM, Filesystem Analysis, Device Forensics

**Methodology**:
1. Mounted SD card image in controlled Linux environment
2. Analyzed Raspberry Pi boot partition structure
3. Examined startup scripts and configuration files
4. Located hardcoded malicious URL in boot sequence

**Key Finding**: IOC embedded in device startup script - potential insider threat tool

</details>

**🎓 Key Learnings**:
- Embedded device security analysis
- Linux forensics techniques
- TinyPilot device architecture understanding
- Insider threat detection in IoT devices

---

## 🛠️ Tools and Techniques

<div align="center">

### 🔍 **Analysis Tools**
![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=flat-square&logo=wireshark&logoColor=white)
![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat-square&logo=powershell&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

### 🔧 **Specialized Tools**
![Registry Explorer](https://img.shields.io/badge/Registry%20Explorer-0078D4?style=flat-square&logo=windows&logoColor=white)
![CyberChef](https://img.shields.io/badge/CyberChef-FF6B35?style=flat-square&logo=chef&logoColor=white)
![Tshark](https://img.shields.io/badge/Tshark-1679A7?style=flat-square&logo=wireshark&logoColor=white)

</div>

### 📊 Techniques Mastered

| Category | Skills Developed |
|----------|------------------|
| **Network Analysis** | DNS tunneling detection, PCAP analysis, C2 identification |
| **Email Forensics** | Header analysis, SMTP log investigation, domain spoofing |
| **System Forensics** | Registry analysis, process investigation, endpoint telemetry |
| **Data Recovery** | Archive extraction, encoding/decoding, credential discovery |
| **Git Forensics** | Repository analysis, commit investigation, supply chain security |
| **Social Engineering** | Negotiation tactics, psychological principles, crisis communication |

---

## 📈 Key Learnings

### 🎯 Technical Skills Gained
- **Network Security**: Advanced PCAP analysis and DNS tunneling detection
- **Digital Forensics**: Multi-platform evidence correlation and timeline analysis  
- **Threat Intelligence**: IOC identification and threat actor behavior analysis
- **Incident Response**: Systematic investigation methodology and evidence preservation

### 🧠 Strategic Insights
- **Holistic Thinking**: Complex challenges require multi-tool, multi-perspective approaches
- **Attention to Detail**: Single character errors can compromise entire investigations
- **Systematic Approach**: Methodical evidence collection prevents overlooked clues
- **Tool Diversity**: Different challenges require specialized forensic tools

### 🚀 Personal Growth
- **Resilience**: Learned to approach unsolved challenges as learning opportunities
- **Documentation**: Comprehensive writeups enhance knowledge retention and sharing
- **Community**: CTF participation builds valuable cybersecurity networks
- **Confidence**: First CTF success established a foundation for continued security research

---

## 📄 License & Usage

This repository is for **educational purposes** and knowledge sharing within the cybersecurity community. All write-ups represent original analysis and investigation work.

**⚠️ Ethical Use Only**: These techniques should only be applied in authorized, legal environments for legitimate security research and education.

---
