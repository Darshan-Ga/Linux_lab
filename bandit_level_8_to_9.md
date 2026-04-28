# OverTheWire Bandit: Level 8 → Level 9
**Target:** `bandit8.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit9`.  
The password is stored in `data.txt` and is the only line of text that **occurs exactly once**.

## 🛠️ The Challenge
After logging in, `ls` again revealed a single file — `data.txt`.

```bash
bandit8@bandit:~$ ls
data.txt
```

But this time, `grep` won't help — we have no keyword to search for.
The file contains many lines of scrambled text, most of which are **duplicates**.
The password is the **one unique line** that appears only once in the entire file.
Finding it manually would be impossible.

## 🧠 How I Solved It

**The Command:**
```bash
bandit8@bandit:~$ strings data.txt | sort | uniq -u
[INSERT YOUR PASSWORD HERE]
```

This is a **three-command pipeline**, each tool feeding its output into the next.

**Breaking down the pipeline:**

| Command | Role |
|---------|------|
| `strings data.txt` | Extract all human-readable strings from the file |
| `sort` | Sort all lines alphabetically, grouping duplicates together |
| `uniq -u` | Print only lines that appear **exactly once** |

**Why each step is necessary:**

**`strings`** — Even though `data.txt` is a text file here, `strings` is a good
habit when dealing with files that may contain binary noise. It extracts only
printable character sequences, giving clean input to the next command.

**`sort`** — This is the critical middle step. `uniq` can only detect adjacent
duplicate lines — it doesn't scan the whole file at once. Sorting first guarantees
that all identical lines are grouped together, so `uniq` can do its job correctly.
Skipping `sort` would cause `uniq` to miss duplicates that aren't consecutive.

**`uniq -u`** — The `-u` flag means "unique only" — it suppresses all lines that
appear more than once and prints only the lines with no duplicates. Without `-u`,
`uniq` would just collapse duplicates into one copy each, which isn't what we want.

The pipeline returned exactly **one line** — the password. ✅

## 💡 Key Takeaways

**`sort | uniq` is a classic Linux combo.**  
You'll see this pattern constantly in shell scripting and CTFs. `sort` prepares
the data; `uniq` processes it. They're designed to work together.

**`uniq -u` vs `uniq -d` — know the difference:**

| Flag | Behaviour |
|------|-----------|
| `uniq` (no flag) | Collapse duplicates, print one copy of each line |
| `uniq -u` | Print **only** lines that appear exactly once |
| `uniq -d` | Print **only** lines that are duplicated |

For this challenge, `-u` is exactly what we need.

**Pipes (`|`) are the Unix philosophy in action.**  
Small, focused tools chained together solve complex problems elegantly.
`strings`, `sort`, and `uniq` each do one thing — combined, they isolate
a single line from thousands in under a second.

## 📸 Evidence

![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/af1712b0c81b722e54057e77f8e91ee30af984b7/bandit%20level%208.png)
![imge alt](https://github.com/Darshan-Ga/Linux_lab/blob/af1712b0c81b722e54057e77f8e91ee30af984b7/bandit%20level%208(2).png)
