# OverTheWire Bandit: Level 15 → Level 16
**Target:** `bandit15.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit16`.  
Same concept as Level 14 — submit the current password to a local service.
But this time the service uses **SSL/TLS encryption** on port 30001.
Plain `nc` won't work here. We need `openssl`.

## 🛠️ The Challenge
After logging in, the home directory is empty again.

```bash
bandit15@bandit:~$ ls
bandit15@bandit:~$
```

Trying `nc localhost 30001` would connect but fail — the service expects
an encrypted SSL/TLS handshake first. Any plain text sent to it gets
rejected. We need a client that speaks SSL.

## 🧠 How I Solved It

**The Command:**
```bash
bandit15@bandit:~$ echo "[current password]" | openssl s_client -connect localhost:30001 -quiet
Correct!
[INSERT NEXT PASSWORD HERE]
```

**Breaking it down:**

| Component | Meaning |
|-----------|---------|
| `echo "[password]"` | Print the current password as output |
| `\|` | Pipe it as input to openssl |
| `openssl s_client` | SSL/TLS client — connects using encrypted channel |
| `-connect localhost:30001` | Target host and port |
| `-quiet` | Suppress the TLS handshake noise, show only the response |

Without `-quiet`, `openssl` dumps the full TLS session details —
certificate info, cipher suites, session tickets, hex dumps — before
showing the actual server response. The `-quiet` flag cuts all that
and shows just what the server sends back.

## 💡 What is SSL/TLS?

SSL (Secure Sockets Layer) and its successor TLS (Transport Layer
Security) are cryptographic protocols that encrypt communication
between two endpoints. When you visit `https://` websites, TLS is
what's protecting your data in transit.
```
Without TLS (plain nc):
┌──────────┐                    ┌──────────┐
│  Client  │── "my password" ──▶│  Server  │
└──────────┘   (anyone can      └──────────┘
see this)
With TLS (openssl s_client):
┌──────────┐                    ┌──────────┐
│  Client  │── x8$#@!Kp2&... ──▶│  Server  │
└──────────┘   (encrypted,      └──────────┘
unreadable)
```
**TLS Handshake — what happened behind the scenes:**
1. Client says hello → "I support these cipher suites"
2. Server responds  → "Use this one, here's my certificate"
3. Keys exchanged   → Session encryption established
4. Encrypted tunnel → Your password travels safely inside

**Key distinction:**

| | `nc` (Level 14) | `openssl s_client` (Level 15) |
|--|-----------------|-------------------------------|
| **Encryption** | ❌ None | ✅ TLS |
| **Use case** | Plain TCP services | HTTPS, SMTPS, encrypted services |
| **Handshake** | None | Full TLS negotiation |
| **Real world** | Internal tools | Every modern web service |

## 💡 Key Takeaways

**`openssl s_client` is `nc` for encrypted services.**  
The mental model is identical to Level 14 — connect, send data,
receive response. The only difference is TLS sits in between.
This is the tool you reach for whenever `nc` connects but gets
no useful response.

**Self-signed certificates are normal in CTFs and internal tools.**  
The output showed `Verify return code: 18 (self-signed certificate)`.
This means the server's certificate wasn't issued by a trusted
Certificate Authority — common in internal/lab environments.
In production, self-signed certs on public services are a red flag.

**TLS is everywhere in cloud security.**  
Every HTTPS connection, every encrypted API call, every secure
database connection uses TLS under the hood. Understanding what
the handshake does and how to interact with TLS services from
the terminal is a foundational cloud security skill.

**`-quiet` is your friend.**  
The raw `openssl s_client` output is verbose and useful for
debugging TLS issues — cipher negotiation, certificate chains,
session details. In CTFs you suppress it with `-quiet`. In real
security work you read it carefully to audit TLS configurations.

## 📸 Evidence
![Bandit Level 15 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/fa632b152ba9a579d2201f4af1d8903607def7d6/bandit%20level%2015.png)
![Bandit Level 15 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/fa632b152ba9a579d2201f4af1d8903607def7d6/bandit%20level%2015(2).png)


