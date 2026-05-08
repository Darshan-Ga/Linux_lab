# OverTheWire Bandit: Level 14 → Level 15
**Target:** `bandit14.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit15`.  
The password can be retrieved by submitting the **current level's password**
to a service listening on **localhost port 30000**.

## 🛠️ The Challenge
After logging in, `ls` returned nothing useful — empty home directory.

```bash
bandit14@bandit:~$ ls
bandit14@bandit:~$
```

The hint tells us there is a service running locally on port 30000 that
is waiting for input. Send it the current password, it gives back the next one.
This is the first level that introduces **network communication** directly
from the terminal.

## 🧠 How I Solved It

**The Command:**
```bash
bandit14@bandit:~$ echo "[current password]" | nc localhost 30000
Correct!
[INSERT NEXT PASSWORD HERE]
```

**Breaking it down:**

| Component | Meaning |
|-----------|---------|
| `echo "[password]"` | Print the current level's password as output |
| `\|` | Pipe — sends that output as input to the next command |
| `nc` | Netcat — connects to a network service and sends/receives data |
| `localhost` | The same machine we are already on |
| `30000` | The port number the service is listening on |

The server responded with `Correct!` followed by the next password —
confirming it received and validated the input successfully.

## 💡 What is Netcat (`nc`)?

Netcat is often called the **"Swiss Army knife of networking"**. At its
core it opens a raw TCP or UDP connection between two endpoints and
lets you send and receive data manually — no protocol overhead, no
browser, just raw socket communication.
```
┌─────────────────────┐         ┌─────────────────────┐
│   Your Terminal     │         │   localhost:30000   │
│                     │  TCP    │                     │
│  echo "password" ──────────▶  │  Validates input    │
│                     │         │  Returns password ──▶│
└─────────────────────┘         └─────────────────────┘
```
**What Netcat can do:**

| Use Case | Example |
|----------|---------|
| Connect to a service | `nc localhost 30000` |
| Listen for connections | `nc -l -p 1234` |
| Transfer files | `nc host 1234 < file.txt` |
| Port scanning | `nc -zv host 1-1000` |
| Banner grabbing | `nc host 80` then `HEAD / HTTP/1.0` |

## 💡 Key Takeaways

**Ports are doors, services are behind them.**  
Port 30000 had a service sitting behind it waiting for the correct
input. This is exactly how real networked applications work —
a web server listens on port 80, SSH on port 22, this validator
on port 30000. Understanding ports is fundamental to networking
and security.

**`nc` is a core security tool.**  
You will use Netcat constantly in CTFs and in real security work —
for banner grabbing, testing open ports, transferring files between
machines, and setting up reverse shells. This level is your introduction
to it in its simplest form.

**Piping into network tools is powerful.**  
`echo "data" | nc host port` is a pattern you will reuse constantly.
It lets you script and automate network interactions without needing
a browser or dedicated client. The same pattern works with `openssl`,
`curl`, and other network tools.

**localhost vs external.**  
The service only accepts connections from the same machine — that is
what `localhost` (127.0.0.1) means. This is a common security pattern:
sensitive internal services bind only to localhost so they are not
exposed to the outside network.

## 📸 Evidence
![Bandit Level 14 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/76382d9517f704bef1321a0278be9bf0caec2749/bandit%20level%2014.png)
![Bandit Level 14 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/76382d9517f704bef1321a0278be9bf0caec2749/bandit%20level%2014(2).png)
