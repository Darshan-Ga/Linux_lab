# OverTheWire Bandit: Level 10 → Level 11
**Target:** `bandit10.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit11`.  
The password is stored in `data.txt`, which contains **Base64 encoded data**.

## 🛠️ The Challenge
After logging in, `ls` showed the now-familiar `data.txt`.

```bash
bandit10@bandit:~$ ls
data.txt
```

Opening it with `cat` reveals a long, garbled-looking string — not binary
garbage this time, but a wall of seemingly random alphanumeric characters.
This is the signature look of **Base64 encoding**.

```bash
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIHdt...
```

## 🧠 How I Solved It

**The Command:**
```bash
bandit10@bandit:~$ cat data.txt | base64 -d
The password is [INSERT YOUR PASSWORD HERE]
```

No filtering needed. The decoded output directly states the password.

**Breaking it down:**

| Command | Role |
|---------|------|
| `cat data.txt` | Read the Base64 encoded contents of the file |
| `base64 -d` | Decode the Base64 string back into plain text |

The `-d` flag stands for **decode**. Without it, `base64` encodes input instead
of decoding it — the opposite of what we want here.

## 💡 What is Base64?

Base64 is an **encoding scheme**, not encryption. It converts binary or text data
into a safe, ASCII-only string using 64 printable characters (A–Z, a–z, 0–9, +, /).

**Key distinction — Encoding vs Encryption:**

| | Encoding | Encryption |
|--|----------|------------|
| **Purpose** | Format conversion | Data protection |
| **Reversible?** | Yes, by anyone | Only with the key |
| **Example** | Base64, URL encoding | AES, RSA |
| **Security** | ❌ None | ✅ Strong |

Base64 is used everywhere — email attachments, image embedding in HTML/CSS,
JWT tokens, and API data transfer. It is **not** a security measure. Anyone
can decode it instantly, as this level demonstrates.

**How to spot Base64:**
- Ends with `=` or `==` padding characters
- Only contains `A–Z`, `a–z`, `0–9`, `+`, `/`
- Length is always a multiple of 4

## 💡 Key Takeaways

**Encoding ≠ Encryption.**  
This is one of the most important distinctions in cybersecurity. Seeing Base64
does not mean data is protected — it just means it was formatted for safe
text transport. Never store passwords or secrets in Base64 and call it secure.

**`base64 -d` is instant decoding.**  
No tools, no online decoders needed. It's built into every Linux system.
You can also encode with `base64` (no flag) and decode with `base64 -d`.

**Recognizing encoding schemes is a core CTF skill.**  
Base64 is just the beginning. As you progress through Bandit and beyond,
you'll encounter ROT13, hex encoding, URL encoding, and more. Identifying
the encoding type is always step one.

## 📸 Evidence

![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/910317de82ab18e3619adba7bb376bf0ef6db134/bandit%20level%2010.png)
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/910317de82ab18e3619adba7bb376bf0ef6db134/bandit%20level%2010(2).png)
