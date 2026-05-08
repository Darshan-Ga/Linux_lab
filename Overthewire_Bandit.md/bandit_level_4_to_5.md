# OverTheWire Bandit: Level 4 → Level 5

**Target:** `bandit4.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit5`. 
The password is saved in the `inhere` directory, but there is a catch: it is hidden inside the **only human-readable file**. 
All the other files contain raw, unreadable binary data.

## 🛠️ The Challenge

Upon logging in and navigating to the `inhere` directory, I found 10 files named from `-file00` to `-file09`. 

```bash
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```
## 🧠 How I Solved It
The primary challenge here is the leading hyphen (-) in the filenames. 
If you try to read them normally (e.g., cat -file01), the terminal interprets the - as a command flag and throws an "invalid option" error.

To bypass this syntax trap, I used a relative path by prepending ./ to the filename. 
This forces the shell to treat the string as a literal file located in the current directory.

**Manual Enumeration Strategy:**
Knowing the correct syntax (cat ./-file00), I decided to systematically go through the files one by one. 
I expected most to output raw binary data, which they did, temporarily scrambling the terminal output with unreadable characters.

I persistently cat'd my way down the list:
```bash
bandit4@bandit:~/inhere$ cat ./-file00
# [Binary Gibberish Output]

bandit4@bandit:~/inhere$ cat ./-file01
# [Binary Gibberish Output]

bandit4@bandit:~/inhere$ cat ./-file02
# [Binary Gibberish Output]
```
I pushed through files 03, 04, 05, and 06. Finally, executing the command on -file07 returned exactly what I was looking for: a clean, 
human-readable text string containing the password!
```bash
bandit4@bandit:~/inhere$ cat ./-file07
[INSERT YOUR PASSWORD HERE]
```
## 📸 Evidence
![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/c1629b816824b655317cdc1b9da27c626eb37780/bandit%20level4.png)


![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/c1629b816824b655317cdc1b9da27c626eb37780/bandit%20level4(2).png)

