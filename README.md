# 🛡️ WiCyS Target Defense Challenge 2025 – Writeups

My writeups and notes for the **WiCyS Target Defense Challenge 2025**.  
This was my **first-ever CTF**, and out of 12 challenges, I solved **11 within one month**.  
I ranked **25th out of 896 challengers**, which qualified me for Tier 2 taking place on the **August 21st**. 🚀

---

## 📖 Overview
I had the incredible opportunity to participate in the WiCyS Tier 1 Target Defense Challenge 2025.  
This journey introduced me to new areas of cybersecurity, from packet analysis and system forensics to investigating insider threats.

✨ **Highlights:**
- 🏆 Solved **11/12 challenges**    
- 🔍 Most memorable: **Challenge D12 – SD card forensic analysis**   

---

## 📂 Table of Contents
- [D1 – Mystery Mail](#d1--mystery-mail)
- [D2 – Not-so-Simple Mail Protocol](#d2--not-so-simple-mail-protocol)
- [D3 – Ransom Wrangler](#d3--ransom-wrangler)
- [D4 – Trout of Office](#d4--trout-of-office)
- [D5 – Ahoy, PCAP 'n](#d5--ahoy-pcap-n)
- [D6 – Smuggled Away!](#d6--smuggled-away)
- [D7 – Endpoints and Exfiltration](#d7--endpoints-and-exfiltration)
- [D8 – Shadow Commit](#d8--shadow-commit)
- [D9 – Logging for Truth](#d9--logging-for-truth)
- [D10 – Backup Break-in](#d10--backup-break-in)
- [D11 – Semi-Final Boss](#d11--semi-final-boss)
- [D12 – Final Boss](#d12--final-boss)

---

## 📨 D1 – Mystery Mail
**Challenge Overview**  
In this scenario context, I am a member of the Personalyze.io's Cybersecurity team and was notified of an extortion email in my inbox. This extortion email claimed to have stolen sensitive company data and demanded a ransom by threatening to release the data if the demand is not met within 48 hours. I needed to analyze the email headers and determine the sender’s original IP.  

**Approach & Solution**  
- Opened the `.eml` file of the extortion email in Notepad to inspect the raw details  
- I scanned and inspected the header section for the sender IP  
- I then identified **252.44.98.29** as the originating IP, and it is associated with the email `sgreen123gwagm.co`

  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/34c2d07f-09a6-47dc-a8ef-336cc04c7552" />


**Lessons Learnt**  
- Attention to detail in headers is essential  
- Context matters when interpreting evidence  

---

## 📧 D2 – Not-so-Simple Mail Protocol
**Challenge Overview**  
Still investigating the extortion attempts, I was tasked with uncovering **evidence of an earlier email** from the same threat actor by digging into the **SMTP logs** within the Insightful Horizon dashboard to find the first extortion message.  

**Approach & Solution**  
- I logged into the Insightful Horizon dashboard and began filtering logs by the known domain `gwagm.co` and the term data.  
- Eventually, I discovered a modified domain: **tgwanagm.co**.  
- In that log entry, the subject line read: *“Warning: We have acquired sensitive data”* with the sender’s email address as **tharris456@tgwanagm.co**.

<img width="800" height="800" alt="image" src="https://github.com/user-attachments/assets/189a8587-0a19-431b-a1f6-24337304215e" />


**Lessons Learnt**  
- Filtering logs requires critical thinking and persistance  
- Threata ctors often make subtle domain variations to bypass detection 

---

## 💰 D3 – Ransom Wrangler
**Challenge Overview**  
This was an interesting challenge. Because the threat actor demanded a large ransom in Bitcoin, my task was to negotiate with the threat actor to reduce the ransom below **30 BTC** while also extending the payment deadline. 
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/d9ac60bb-6d1a-46eb-b6ed-68701792be81" />

**Approach & Solution**  
- Social engineering was used to persuade and engage tactics with the threat actor, it was quite difficult to apply these tactics.
  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/2239dea3-aaad-45dc-8bf9-5ad23fcbbb9f" />

- I shifted the focus toward compromise, suggesting they would get paid faster if the ransom was lower by reducing the ransom to **25 BTC**  
- Extracted flag: `CTF-RAN-FA5123FF: CTF-DEA-E86ED89E`  

**Lessons Learnt**  
- Social engineering can change outcomes in cybersecurity  
- Negotiation skills matter, even in technical fields  

---

## 🎣 D4 – Trout of Office
I couldn’t solve this challenge in time, but reviewing the walkthrough showed me **exactly where I went wrong** and how to approach it differently next time. I have attached my version of the walkthrough below:   

### 📝 Trout of Office Walkthrough

There are a lot of logs of varying things, so let's separate them into two different categories:

- **zekes-logs-...** – logs set up by Zeke, with a fishy theme. Each type maps to specific data:
  - **salmon** – first names  
  - **trout** – last names  
  - **cod** – street addresses  
  - **mackerel** – cities  
  - **halibut** – states  
  - **walleye** – zip codes  
  - **snapper** – credit card numbers (last 4 digits only)  
  - **tuna** – confusing noise data (ignore this one!)  

- **http-logs** – HTTP traffic to access the Personalyz.io application.

### 🔎 Tracking Down the Victim's Data

The process is mostly the same for each type of information. We’ll start with the first name.

#### 🧩 First Name

1. Open the **zekes-logs-salmon** log in the Insightful Horizon dashboard.  
2. Search for the victim’s first name. Example: `"John"`.  
3. If nothing shows up, note that names are **prefixed with a letter**. Try wildcard searches: 
4. Look for clues:
   - Sockeye Salmon weight limits (7–8 kg → 7000–8000 grams).
   - Fields like fnq... or alta with numeric values.
5. Filter visually for numbers in the range 7000–8000.

#### 🧩 Last Name

1. Search for the victim’s last name, e.g. "Doe".
2. Use a wildcard prefix search:.
3. Look for clues:
   - “Sharks and trout” hint → check the shark field.
   - Filter records where shark values are between 7000 and 8000.
4. Make a note of each shark + _vista__X... pair for later.

#### 🧩 Address
- The process is similar to names, but zip codes are stored as IDs. You’ll also need credit card info, which works the same way.

#### 🌐 HTTP Logs – Pivoting to Requests
At this step, switch to http-logs.
We’re looking for requests without a User-Agent header (Zeke wouldn’t use a GenAI agent).
1. Open the http-logs in the dashboard
2. Filter out requests with User-Agent
   - After filtering, you should have around 5 hits. 

#### 🔗 Assembling the Data (so putting everything together)
Now check each request to see if it contains useful info. Some values are query parameters, others are in the URI.
Look for paths like:

/apps_per-SAPSOFT/p/

This takes two UUID-like IDs. Try inserting the IDs you found earlier for first and last names.

##### For the first try
<pre>curl -X GET "https://target-flask.chals.io/apps_per-SAPSOFT/p/1234/5678" </pre> 

##### If first try fails, then reverse the order
<pre> curl -X GET "https://target-flask.chals.io/apps_per-SAPSOFT/p/5678/1234"  </pre> 

1234 = first name ID

5678 = last name ID
 
If that works, you should see an ID returned. Keep it later for API calls.

#### Address API Call
For addresses, look for endpoints like:

/l/a/

Pass in the IDs for:
- Street address (cod)
- City (mackerel)
- State (halibut)
- Zip code (walleye)

---

## 🌐 D5 – Ahoy, PCAP 'n
**Challenge Overview**  
For this challenge, I was tasked with investigating how a threat actor was exfiltrating sensitive company data and whether they were still active in our network. I did this by analysing the provided PCAP file to find the hostname of compromised machine and the Command and Control(C2) IP adress the attacker was using to recieve the leaked data.  

**Approach & Solution**  
- I opened the PCAP in Wireshark and applied filters to focus on DNS traffic and paid attention to abnormal query patterns.
<img width="550" height="550" alt="image" src="https://github.com/user-attachments/assets/f88df4d6-cbf1-4dfd-afa8-65049983ca2c" />

- I noticed quite a few odd domain requests that were all irrelevant to each other, which led me to thinking I have stumbled what appears to be the use of DNS tunneling. Most of these came from an IP address of 10.75.34.13 and sending to an IP of 251.91.13.37, and by observing the response packets, a hostname of bvlik was found. 

- Identified compromised host: **bvlik**  
- C2 IP: **251.91.13.37**  

**Lessons Learnt**  
- DNS can be abused for stealthy exfiltration  
- Wireshark is valuable for packet analysis  
- Attackers can hide in plain sight with minimal traces  

---

## 📡 D6 – Smuggled Away!
**Challenge Overview**  
In this challenge, I had to extract the stolen data (credit card expiration, CVV, email) hidden in DNS queries.  

**Approach & Solution**  
- Filtered suspicious subdomains in Wireshark ip.src == 10.75.34.13 && ip.dst == 251.91.13.37
  <img width="1169" height="614" alt="image" src="https://github.com/user-attachments/assets/dc0b1e17-1610-4990-abf7-73ef4b00b6e1" />
  <img width="429" height="506" alt="image" src="https://github.com/user-attachments/assets/395f01c7-4c03-4839-a6ff-8c80fed732a5" />
- I then extracted the suspicious looking subdomains by using Tshark, the command-line version of Wireshark via Powershell.
<img width="1586" height="700" alt="image" src="https://github.com/user-attachments/assets/b5f691c4-1e09-401e-9eeb-595926e7c76a" />

  and then I ran the command
  <pre> & "C:\Program Files\Wireshark\tshark.exe" -r "C:Desktop\pirates.pcap" -Y "ip.dst == 251.91.13.37 && dns.qry.name" -T fields -e dns.qry.name | Where-Object { ($_ -split '\.')[0] -match '^[a-zA-Z0-9]{5,}$' } | ForEach-Object { ($_ -split '\.')[0] }   </pre>

  which extracts the DNS query names and filters only the subdomains we needed, it also removes the rest of the domain we do not need such as github.com or vimeo.com. I also combined all together using the command

  <pre>($(& "C:\Program Files\Wireshark\tshark.exe" -r "C:Desktop\pirates.pcap" -Y "ip.dst == 251.91.13.37 && dns.qry.name" -T fields -e dns.qry.name | Where-Object { ($_ -split '\.')[0] -match '^[a-zA-Z0-9]{5,}$' } | ForEach-Object { ($_ -split '\.')[0] })) -join "" </pre>

  which gave us the following
  <pre> d6fqqaecfjjgqax7bxglcducgaiabuhz73remhou332tqyetdajb2zeqzgyway2mfzenv6x76ia665iwm4mk77pd3ygsbjbv6yqrp5hjqxr7us3qrffutqpqs3w3hqxqasrjuglwjtkr4g27dxmloddblphhtgw762oyehmxldaaxk4iunlbwjjbochhjqzh577bt4hmlrzqaaaa
 </pre>

I then capitalised this string to give us the following and we will see later why.
<pre> D6FQQAECFJJGQAX7BXGLCDUCGAIABUHZ73REMHOU332TQYETDAJB2ZEQZGYWAY2MFZENV6X76IA665IWM4MK77PD3YGSBJBV6YQRP5HJQXR7US3QRFFUTQPQS3W3HQXQASRJUGLWJTKR4G27DXMLODDBLPHHTGW762OYEHMXLDAAXK4IUNLBWJJBOCHHJQZH577BT4HMLRZQAAAA </pre>

- Used **CyberChef** to decode from Base32, which requires the string to be uppercase and consist of number from 2-7 which we have, and then I applied the Gunzip option to uncompress the string
<img width="1912" height="551" alt="image" src="https://github.com/user-attachments/assets/6b887c23-ddba-49a9-a168-4c69ba611d43" />

- Successfully reconstructed sensitive data: Alec	SHERMAN	4167 East 3rd Spur	Central Islip	NY	11722	(215) 835-2392	alec@sbcglobal.net	342644019686141	0016	11/30   

**Lessons Learnt**  
- DNS traffic can contain encoded data exfiltration, which is another form of a cyberattack used to steal data seen in this scenario   
- CyberChef is a must-have decoding tool  
- One single missing letter can ruin the entire decryption, so I do not recommend extracting manually, ever.   

---

## 🖥️ D7 – Endpoints and Exfiltration
**Challenge Overview**  
Identify user, process, and software responsible for exfiltration using `lsof`, `ps`, and `history` outputs.  

**Approach & Solution**  
- Correlated IP from D5 with lsof connections  
- Confirmed process via ps output  
- Traced obfuscated filename in history file  

**Lessons Learnt**  
- Endpoint telemetry reveals hidden activity  
- Cross-referencing multiple logs paints a complete picture  
- Threat actors often disguise tools under benign names  

---

## 🔎 D8 – Shadow Commit
**Challenge Overview**  
Analyze `.git` directory history to identify malicious commit introducing an IP.  

**Approach & Solution**  
- Used `git log` and `git diff`  
- Found commit with hardcoded malicious IP  
- Extracted commit hash + IPv4 address  

**Lessons Learnt**  
- Git commit history can expose supply chain compromise  
- Understanding Git tools is essential for forensic developers  

---

## 📜 D9 – Logging for Truth
**Challenge Overview**  
Verify whether developer Erik really authored a shady commit or was framed.  

**Approach & Solution**  
- Used Insightful Horizon logs  
- Filtered audit logs over 6 months  
- Found commit tied to suspicious IP not belonging to Erik  

**Lessons Learnt**  
- Commit history ≠ proof of authorship  
- Audit logs are crucial for attribution  

---

## 💾 D10 – Backup Break-in
**Challenge Overview**  
Find Git committer’s leaked credentials in backup server files.  

**Approach & Solution**  
- Extracted `.tar.gz` archive  
- Searched plaintext configs  
- Found password starting with `wicys`  

**Lessons Learnt**  
- Backup servers often expose sensitive data  
- Simple text searches can reveal critical evidence  

---

## 🗝️ D11 – Semi-Final Boss
**Challenge Overview**  
Analyze Windows Registry hive for persistence keys on “clean” host.  

**Approach & Solution**  
- Loaded hive in **Registry Explorer**  
- Investigated `Run`, `Services`, and `Winlogon` keys  
- Found suspicious persistence key linked to non-native executable  

**Lessons Learnt**  
- Registry artifacts are attacker footprints  
- Specialized forensic tools are vital for safe analysis  

---

## 🎮 D12 – Final Boss
**Challenge Overview**  
Investigate forensic image of SD card tied to TinyPilot device.  

**Approach & Solution**  
- Mounted SD card image in Linux VM  
- Found Raspberry Pi boot partition  
- Located IOC: **hardcoded URL in startup script**  

**Lessons Learnt**  
- Embedded devices can be repurposed for insider threats  
- Linux knowledge is critical for deep-dive forensics  
- TinyPilot tools need monitoring to prevent abuse  

---



