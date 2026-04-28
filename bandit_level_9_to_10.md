# OverTheWire Bandit: Level 9 → Level 10

**Target:** `bandit9.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit10`.  
The password is stored in `data.txt` among a few human-readable strings,
preceded by **several `=` characters**.

## 🛠️ The Challenge
After logging in, `ls` showed a familiar sight — `data.txt`.

```bash
bandit9@bandit:~$ ls
data.txt
```

But this time the file is mostly **binary data**, not plain text. Running
`cat data.txt` floods the terminal with unreadable garbage. We need to first
extract only the human-readable parts, then filter for the `===` marker.

## 🧠 How I Solved It

**The Command:**
```bash
bandit9@bandit:~$ strings data.txt | grep "==="
========= the
========= password
========= is
=========  [INSERT YOUR PASSWORD HERE]
```

**Breaking down the pipeline:**

| Command | Role |
|---------|------|
| `strings data.txt` | Extract all printable human-readable strings from the binary file |
| `grep "==="` | Filter only lines containing `===`, matching the password marker |

The output literally spells it out across four lines:  
`========= the`, `========= password`, `========= is`, `========= [password]`

The last line's value after the `=========` is the password.

## 💡 Key Takeaways

**`strings` is essential for binary files.**  
When `cat` produces garbage, `strings` is your first move. It scans any file —
binary or not — and extracts sequences of printable characters above a minimum
length (default: 4 characters). It's a staple tool in forensics and CTFs alike.

**`strings` + `grep` is a powerful combo.**  
You'll use this pairing constantly in later Bandit levels and real-world
binary analysis. Extract readable content first, then filter for what matters.

**The clue was literal.**  
The level told you the password is next to `=` signs. Grepping for `===` was
the direct translation of that hint into a command. In CTFs, always read the
objective carefully — it often contains the exact filter you need.

## 📸 Evidence

![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/b4861e627dab480a4c2fab6b92602208f0d7ccaa/bandit%20level%209.png)
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/b4861e627dab480a4c2fab6b92602208f0d7ccaa/bandit%20level%209(2).png)
