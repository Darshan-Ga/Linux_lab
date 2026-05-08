# OverTheWire Bandit: Level 3 → Level 4

**Target:** `bandit3.labs.overthewire.org`
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit4`. The password is saved in a hidden file located within the `inhere` directory.

## 🧠 Concepts Covered
* **Directory Navigation:** Using `cd` (change directory) to move through the file system.
* **Hidden Files (Dotfiles):** Understanding that files beginning with a dot (`.`) are hidden from standard directory listings.
* **Command Flags:** Modifying the behavior of the `ls` command using flags like `-a` (all) or `-la` (long format, all).

## 🛠️ Step-by-Step Resolution

### Evudense 
I connected to the Bandit server using SSH as `bandit4` and authenticated using the password retrieved from Level 3.

![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/4115e643d2d742b9472592788b26cfb00e5f7031/bandit%20level3.png) 
![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/4115e643d2d742b9472592788b26cfb00e5f7031/bandit%20level3(2).png) 



### Step 1: Investigating the Home Directory
Once logged in, I used the `ls` command to list the contents of the current directory. 

```bash
bandit3@bandit:~$ ls
inhere
```
The output revealed a single directory named inhere.

### Step 2: Navigating into the Directory
To look inside, I changed my current working directory to inhere using the cd command, and then ran ls again to see what was inside.

```bash
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
```
The ls command returned nothing, making the directory appear empty.

### Step 3: Revealing Hidden Files
In Linux, files and directories that start with a period (e.g., .filename) are hidden by default. To view them, I needed to append the -a (all) flag to the ls command. I prefer using ls -a to see the hidden files.

```bash
bandit3@bandit:~/inhere$ ls -a
. .. ...Hiding-from-you
```
This revealed the file named ...Hiding-from-you.

### Step 4: Extracting the Password
Now that the filename was visible, I used the cat command to read the contents of the .hidden file and retrieve the password for Level 4.

```bash
bandit3@bandit:~/inhere$ cat ...Hiding-from-you
```








