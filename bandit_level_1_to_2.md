# 🚩 Bandit Level 1 → Level 2: Bypassing Shell Parsing & Standard Input Traps

### 🎯 The Mission Context
After securing access as `bandit1`, the objective was to read the password for the next level. 
However, the target file was named `-` (a single dash). 

This challenge is a classic test of Linux fundamentals, 
focusing on how the bash shell tokenizes commands versus how it resolves file paths. 
It highlights a common trap that can cause automated deployment scripts or security tools to hang indefinitely.

---

### 💻 Execution & Terminal Flow

**Step 1: The Standard Input Trap (Failed Attempt)**
My initial attempt was to read the file using the standard syntax. 
```bash
bandit1@bandit:~$ cat -
# The terminal hangs, waiting for user input via stdin. (Aborted with Ctrl+C)
```
### Evidence
![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/cf83b1c3150592dd02a7f9f443b5aac39aaedfe3/bandit%20level%201%E2%86%922.jpg)


![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/cf83b1c3150592dd02a7f9f443b5aac39aaedfe3/bandit%20level%201%E2%86%922(2).jpg)
