# 🚩 Bandit Level 0 → Level 1: Environment Enumeration & Standard Output

### 🎯 The Mission Context
After successfully establishing an SSH connection to the `bandit0` environment, the next objective was to locate and extract the password for the `bandit1` user. The challenge stated the password was stored in a file named `readme` within the home directory. 

While the task is straightforward, it serves as a fundamental exercise in directory enumeration and reading file streams in a headless Linux environment.

---

### 💻 Execution & Terminal Flhttps://github.com/Darshan-Ga/Linux_lab/tree/mainow
Upon logging in, I needed to verify my location in the filesystem and read the target file.

**Step 1: Enumerating the Directory**
Before interacting with any files, I mapped out the current directory to ensure I knew exactly what assets were present.
```bash
bandit0@bandit:~$ ls
readme
```
### Evidence
![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/3345fcdb968d9ae771134b060ab833bfc310f2d6/bandit%20level%200%E2%86%921(2).jpg)


![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/040d13d03dc698b9fc6fa83800169ca8d6a847ab/bandit%20level%200%E2%86%921.jpg)
