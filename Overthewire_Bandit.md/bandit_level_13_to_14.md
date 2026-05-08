# OverTheWire Bandit: Level 13 → Level 14
**Target:** `bandit13.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit14`.  
This level introduces a new concept — instead of a password, you are given
a **private SSH key** to log into the next level directly.

## 🛠️ The Challenge
After logging in, `ls` reveals a single file — not a `data.txt` this time,
but an SSH private key.

```bash
bandit13@bandit:~$ ls
sshkey.private
```

There is no password to find in this directory. The private key itself
is the credential — you use it to authenticate as `bandit14` without
needing a password at all.

## 🧠 How I Solved It

**Step 1 — Use the private key to SSH into bandit14**
```bash
bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost -p 2220
```

**Breaking down the command:**

| Flag | Meaning |
|------|---------|
| `ssh` | Secure Shell — encrypted remote login protocol |
| `-i sshkey.private` | Use this identity file (private key) for authentication |
| `bandit14@localhost` | Log in as user `bandit14` on the same machine |
| `-p 2220` | Connect on port 2220 (non-default SSH port) |

**Step 2 — Read the password directly from the system**

Once logged in as `bandit14`, the password is readable from the
bandit password store:

```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
[INSERT YOUR PASSWORD HERE]
```

## 💡 How SSH Key Authentication Works

Traditional SSH login uses a password. Key-based authentication
uses a **mathematically linked key pair** instead:
```
┌─────────────────┐         ┌─────────────────┐
│   Your Machine  │         │   Remote Server │
│                 │         │                 │
│  Private Key 🔑 │──────▶  │  Public Key 🔓  │
│  (keep secret)  │  match? │  (stored here)  │
└─────────────────┘         └─────────────────┘
```

| | Password Auth | Key Auth |
|--|--------------|----------|
| **Credential** | Something you know | Something you have |
| **Brute-forceable?** | ✅ Yes | ❌ No |
| **Phishable?** | ✅ Yes | ❌ No |
| **Used in production?** | Rarely | Almost always |

The private key never leaves your machine. The server only stores
the public key. Authentication works by cryptographic proof — the
server challenges your client to prove it holds the matching private
key, without the private key ever being transmitted.

## 💡 Key Takeaways

**SSH keys are the industry standard.**  
Almost every cloud server, GitHub repository, and production system
uses key-based SSH authentication. Passwords over SSH are considered
insecure practice in professional environments.

**`-i` flag specifies the identity file.**  
By default SSH looks for keys in `~/.ssh/id_rsa`. The `-i` flag lets
you specify a different key file — essential when working with multiple
keys across different servers or CTF challenges.

**`localhost` means the same machine.**  
You SSH'd from `bandit13` into `bandit14` on the same server using
port 2220. This is a common pattern in CTFs and also in real
infrastructure — jumping between users or services on the same host.

**Private keys must stay private.**  
If someone gets your private key, they have your access. In real
environments, private keys should be passphrase-protected and never
committed to GitHub. This is one of the most common real-world
security mistakes developers make.

## 📸 Evidence
![Bandit Level 13 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/c271c8991b764924c8ea2c1cec23a0c554f8b815/bandit%20level%2013.png)
![Bandit Level 13 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/c271c8991b764924c8ea2c1cec23a0c554f8b815/bandit%20level%2013(2).png)
