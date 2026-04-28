# OverTheWire Bandit: Level 6 → Level 7
**Target:** `bandit6.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit7`.  
The password is stored **somewhere on the server** and meets all three conditions:
- Owned by user **bandit7**
- Owned by group **bandit6**
- Exactly **33 bytes** in size

## 🛠️ The Challenge
After logging in, `ls` returned nothing useful — the home directory was completely empty.

```bash
bandit6@bandit:~$ ls
bandit6@bandit:~$
```

No `inhere` folder. No hints. The file could be **anywhere** on the entire server filesystem.
This rules out any manual approach entirely — we need `find` to sweep the whole system.

## 🧠 How I Solved It

**The Command:**
```bash
bandit6@bandit:~$ find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```

**Breaking down each flag:**

| Flag | Meaning |
|------|---------|
| `/` | Search from the **root** of the entire filesystem |
| `-type f` | Match only regular files |
| `-size 33c` | Exactly 33 bytes in size |
| `-user bandit7` | File must be owned by user `bandit7` |
| `-group bandit6` | File must be owned by group `bandit6` |
| `2>/dev/null` | Redirect all error messages to `/dev/null` (silence them) |

**Why `2>/dev/null` matters:**  
Searching from `/` means `find` will try to enter directories it doesn't have permission
to read — like `/root`, `/proc`, and various system folders. Without this redirect,
the terminal floods with hundreds of `Permission denied` errors, completely burying
the one result you actually need. Redirecting `stderr` (file descriptor `2`) to `/dev/null`
silences all that noise, leaving only the clean output.

The search returned exactly **one match**:
/var/lib/dpkg/info/bandit7.password

This is tucked inside `/var/lib/dpkg/info/` — the package manager's internal metadata
directory. Not somewhere you'd ever look manually.

**Reading the file:**
```bash
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
[INSERT YOUR PASSWORD HERE]
```

Password retrieved. ✅

## 💡 Key Takeaways

**Search scope matters.**  
Level 5 searched `.` (current directory and below). Level 6 searches `/` — the entire
server. One character change, completely different scope. Always match your search root
to where the file could actually be.

**`2>/dev/null` is essential for system-wide searches.**  
On any multi-user Linux system, a root-level `find` without stderr suppression is
almost unusable. This redirect is a standard professional habit, not just a CTF trick.

**File ownership is metadata you can query.**  
`-user` and `-group` flags let you filter by who owns a file. Combined with `-size`,
this makes `find` precise enough to isolate one file out of tens of thousands on
an entire server in under a second.

**The password wasn't "hidden" — it was obscure by location.**  
`/var/lib/dpkg/info/` is a legitimate system path that no one browses manually.
Security through obscurity is not security — but it does illustrate why knowing
your filesystem layout matters.

## 📸 Evidence
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/0a878bdcc40a626b1e57af828acc406c74614116/bandit%20level%206.png)
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/0a878bdcc40a626b1e57af828acc406c74614116/bandit%20level%206(2).png)
