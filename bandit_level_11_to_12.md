# OverTheWire Bandit: Level 11 → Level 12
**Target:** `bandit11.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit12`.  
The password is stored in `data.txt`, where all lowercase and uppercase
letters have been rotated by **13 positions** — a classic cipher known as **ROT13**.

## 🛠️ The Challenge
After logging in, `ls` revealed the familiar `data.txt`.

```bash
bandit11@bandit:~$ ls
data.txt
```

Running `cat data.txt` returns readable text — but the password is scrambled.
Every letter has been shifted 13 places forward in the alphabet, making it
unreadable without reversing the rotation.

## 🧠 How I Solved It

**The Command:**
```bash
bandit11@bandit:~$ cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

**Breaking it down:**

| Component | Meaning |
|-----------|---------|
| `cat data.txt` | Read the ROT13 encoded contents |
| `tr "A-Za-z" "N-ZA-Mn-za-m"` | Translate every letter by shifting it 13 positions |

**How the `tr` mapping works:**

`tr` (translate) replaces characters from the first set with the corresponding
character in the second set, position by position.

```
Input:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Output: N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
```
So `A` becomes `N`, `B` becomes `O`, `N` becomes `A` and so on.
The same mapping applies to lowercase letters simultaneously.

**Why does decoding ROT13 use the same mapping as encoding?**  
Because ROT13 shifts by exactly half the alphabet (26 ÷ 2 = 13).
Applying it twice returns the original text. Encoding and decoding
are the same operation — one of ROT13's elegant properties.

## 💡 What is ROT13?

ROT13 is a simple substitution cipher that replaces each letter with
the one 13 positions after it in the alphabet. It was historically used
in online forums to hide spoilers or punchlines — not for real security.

**ROT13 vs Base64 — two levels, two encoding types:**

| | ROT13 | Base64 |
|--|-------|--------|
| **Type** | Substitution cipher | Encoding scheme |
| **Input** | Letters only | Any data |
| **Security** | ❌ None | ❌ None |
| **Used for** | Obfuscation | Data transport |
| **Decode tool** | `tr` | `base64 -d` |

Both are trivially reversible. Neither is encryption.

## 💡 Key Takeaways

**`tr` is a character-level translation tool.**  
It maps one set of characters to another, one-to-one. Beyond ROT13,
you can use it to convert uppercase to lowercase (`tr "A-Z" "a-z"`),
delete characters (`tr -d`), or squeeze repeats (`tr -s`).

**ROT13 is obfuscation, not protection.**  
It appears in CTFs, old forum posts, and puzzle games. Recognizing
the shifted-letter pattern and reaching for `tr` immediately is a
core CTF instinct to build.

**Encoding schemes compound.**  
Level 10 was Base64. Level 11 is ROT13. Real-world obfuscation often
layers multiple encodings together — you'll decode Base64 to reveal
ROT13 to reveal hex, and so on. Identifying the current layer is
always step one.

## 📸 Evidence
![Bandit Level 11 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/0be7db75e2c6921627ecd663dcfa4cecd514f6ac/bandit%20level%2011.png)
![Bandit Level 11 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/0be7db75e2c6921627ecd663dcfa4cecd514f6ac/bandit%20level%2011(2).png)
