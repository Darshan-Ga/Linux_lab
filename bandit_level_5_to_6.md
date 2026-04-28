# OverTheWire Bandit: Level 5 → Level 6
**Target:** `bandit5.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit6`.  
The password is stored somewhere inside the `inhere` directory, but with a twist —  
it must meet **all three** of the following conditions:
- Human-readable
- Exactly **1033 bytes** in size
- **Not executable**

## 🛠️ The Challenge
After logging in and navigating to the `inhere` directory, I was greeted with **20 subdirectories**,
each named `maybehere00` through `maybehere19`.

```bash
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
```

Manually checking every file inside every subdirectory would be tedious and unreliable.
This is where the `find` command becomes a precision instrument.

## 🧠 How I Solved It

Instead of brute-forcing my way through 20 directories, I used the `find` command to
filter files using all three given conditions simultaneously.

**The Command:**
```bash
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
./maybehere07/.file2
```

**Breaking down each flag:**

| Flag | Meaning |
|------|---------|
| `.` | Search recursively from the current directory |
| `-type f` | Match only regular files (not directories or symlinks) |
| `-size 1033c` | Match files that are exactly 1033 bytes (`c` = bytes) |
| `! -executable` | Exclude executable files (the `!` is a logical NOT) |

The result was instant and unambiguous — exactly **one file** matched all conditions:
`./maybehere07/.file2`

Note the leading dot in `.file2` — this is a **hidden file** in Linux (files prefixed with `.`
are hidden from a normal `ls` listing). Without the `find` command, this file would have been
very easy to miss.

**Reading the file:**
```bash
bandit5@bandit:~/inhere$ cat maybehere07/.file2
[INSERT YOUR PASSWORD HERE]
```

Clean, human-readable output. Password retrieved. ✅

## 💡 Key Takeaways

**`find` is a scalpel, not a sledgehammer.**  
When given multiple filtering conditions, it narrows down thousands of candidates to exactly
the one you need — instantly. Manual enumeration across 20 directories and their contents
would have been error-prone and slow.

**Hidden files are real.**  
The `.file2` naming is a classic Linux trick. Always use `find` or `ls -la` when you suspect
hidden files are in play.

**The `-size` flag uses units.**  
`1033c` means 1033 bytes. Other units include `k` (kilobytes), `M` (megabytes), and `G` (gigabytes).
Knowing this makes `find` dramatically more powerful for forensic-style searches.

## 📸 Evidence
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/a8270d20d47fb2a62dbad346c207608be74fc3fd/bandit%20level%205.png)
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/a8270d20d47fb2a62dbad346c207608be74fc3fd/bandit%20level%205(2).png)
