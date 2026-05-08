# OverTheWire Bandit: Level 7 → Level 8
**Target:** `bandit7.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit8`.  
The password is stored in `data.txt` next to the word **"millionth"**.

## 🛠️ The Challenge
After logging in, `ls` revealed a single file — `data.txt`.

```bash
bandit7@bandit:~$ ls
data.txt
```

Simple enough, right? Not quite. `data.txt` contains tens of thousands of lines,
each formatted as a `word : password` pair. Opening it manually with `cat` would
dump an unscrollable wall of text. You need a way to find one specific word
among thousands — instantly.

## 🧠 How I Solved It

**The Command:**
```bash
bandit7@bandit:~$ grep "millionth" data.txt
millionth       [INSERT YOUR PASSWORD HERE]
```

That's it. One command, one result.

**Breaking it down:**

| Component | Meaning |
|-----------|---------|
| `grep` | Search tool that scans files for lines matching a pattern |
| `"millionth"` | The exact string to search for |
| `data.txt` | The file to search through |

`grep` scans every line in `data.txt` and prints only the line(s) containing the
word `millionth` — returning the password right beside it.

## 💡 Key Takeaways

**`grep` is your best friend for text search.**  
No matter how large the file is — thousands or millions of lines — `grep` finds
your target in milliseconds. `cat`-ing a massive file and reading it manually is
never the answer.

**This level is intentionally straightforward.**  
After the multi-flag `find` commands in Levels 5 and 6, Level 7 is a palette
cleanser. It reinforces a single, essential tool: `grep`. The simplicity is the lesson.

**`grep` is also composable.**  
You can pipe it, invert it (`grep -v`), make it case-insensitive (`grep -i`),
show line numbers (`grep -n`), or search recursively across directories (`grep -r`).
What you used here is just its most fundamental form — and often all you need.

## 📸 Evidence
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/6ea40ca70da82e8fd390f8708412560f1a37e7c2/bandi%20level%207.png)
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/6ea40ca70da82e8fd390f8708412560f1a37e7c2/bandit%20level%207(2).png)
