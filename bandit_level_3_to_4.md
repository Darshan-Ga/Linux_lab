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

### Step 1: Connecting to the Server
First, I connected to the Bandit server using SSH as `bandit4` and authenticated using the password retrieved from Level 3.

![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/4115e643d2d742b9472592788b26cfb00e5f7031/bandit%20level3.png) 
![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/4115e643d2d742b9472592788b26cfb00e5f7031/bandit%20level3(2).png) 



### Step 2: Investigating the Home Directory
Once logged in, I used the `ls` command to list the contents of the current directory. 

```bash
bandit3@bandit:~$ ls
inhere
