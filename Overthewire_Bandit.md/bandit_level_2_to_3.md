# OverTheWire Bandit: Level 2 → Level 3

**Target:** `bandit2.labs.overthewire.org`
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit3`. 
The password is saved in a file located in the home directory, 
but the filename presents a specific challenge: it is named `spaces in this filename`. 

## 🧠 Concepts Covered
* **Command Line Argument Parsing:** Understanding how the bash shell interprets spaces.
* **Escaping Characters:** Using backslashes (`\`) or quotes (`" "`, `' '`) to handle special characters in filenames.
* **Basic Linux Commands:** `ls` (list directory contents) and `cat` (concatenate and print files).

## 🛠️ Step-by-Step Resolution

### Step 1: Connecting to the Server
First, I connected to the Bandit server using SSH as `bandit2` and entered the password obtained from the previous level.

![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/2c07990a04f36b453805d3129fe90a19cc3162e3/bandit_level2.png) 


![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/2c07990a04f36b453805d3129fe90a19cc3162e3/bandit_level2(2).png)


### Step 2: Investigating the Directory
Once logged in, I used the `ls` command to list the contents of the current home directory. 

```bash
bandit2@bandit:~$ ls
spaces in this filename
```

### Step 3: The Challenge with Spaces
If we simply try to read the file using cat spaces in this filename, the command will fail. This is because the bash shell uses spaces to separate arguments. It will attempt to look for four separate files: spaces, in, this, and filename.

```bash
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```

### Step 4: Extracting the Password
To tell the terminal that the entire string is a single filename.

**Method :** Using Quotation Marks
Enclosing the filename in quotation marks tells the shell to treat everything inside them as a single argument.

```bash
bandit2@bandit:~$ cat "spaces in this filename"
```
