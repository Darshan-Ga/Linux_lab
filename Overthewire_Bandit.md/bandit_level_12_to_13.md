# OverTheWire Bandit: Level 12 → Level 13
**Target:** `bandit12.labs.overthewire.org`  
**Port:** `2220`

## 🎯 Objective
The goal of this level is to find the password for `bandit13`.  
The password is stored in `data.txt` — a hexdump of a file that has been
**repeatedly compressed** using multiple formats layered on top of each other.

## 🛠️ The Challenge
This level is a multi-stage decompression puzzle. The file has been compressed
and recompressed multiple times using different tools — `gzip`, `bzip2`, and `tar`.
The trick is that the files are deliberately misnamed to hide their true format.

The `file` command becomes your most important tool here — it reads the actual
file header (magic bytes) to tell you the true format, regardless of the filename.

## 🧠 How I Solved It

**Step 1 — Create a working directory and copy the file**
```bash
bandit12@bandit:~$ mkdir /tmp/tmp.vYcDCLDd0q
bandit12@bandit:~$ cp data.txt /tmp/tmp.vYcDCLDd0q
bandit12@bandit:~$ cd /tmp/tmp.vYcDCLDd0q
```
Always work in `/tmp` on Bandit — you have write permissions there.

**Step 2 — Identify the first layer**
```bash
$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```
The `.bin` extension is misleading. `file` reveals it's actually `bzip2` data.

**Step 3 — Rename and decompress bzip2**
```bash
$ mv data6.bin data6.bz2
$ bzip2 -d data6.bz2
$ ls
data5.bin.tar  data6  data.txt  mystery.tar
```

**Step 4 — Identify the next layer**
```bash
$ file data6
data6: POSIX tar archive (GNU)
```
Now it's a tar archive. Rename and extract.

**Step 5 — Rename and extract tar**
```bash
$ mv data6 data6.tar
$ tar -xvf data6.tar
data8.bin
```

**Step 6 — Identify the next layer**
```bash
$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin"
```
Now it's gzip. Rename and decompress.

**Step 7 — Rename and decompress gzip**
```bash
$ mv data8.bin data8.gz
$ gzip -d data8.gz
$ file data8
data8: ASCII text
```
Finally — plain ASCII text. No more layers.

**Step 8 — Read the password**
```bash
$ cat data8
The password is [INSERT YOUR PASSWORD HERE]
```

## 🔄 The Full Decompression Chain
```
data.txt (hexdump)
└── data6.bin → bzip2 → data6
└── data6.tar → tar → data8.bin
└── data8.gz → gzip → data8
└── ASCII text → PASSWORD ✅
```
## 💡 Command Reference

| Command | What it does |
|---------|-------------|
| `file <filename>` | Reads magic bytes to identify true file format |
| `mv <old> <new>` | Rename file to correct extension before decompressing |
| `bzip2 -d <file>` | Decompress a `.bz2` file |
| `tar -xvf <file>` | Extract a `.tar` archive |
| `gzip -d <file>` | Decompress a `.gz` file |

**Flag breakdown for `tar -xvf`:**

| Flag | Meaning |
|------|---------|
| `-x` | Extract files |
| `-v` | Verbose — show what's being extracted |
| `-f` | Read from the specified file |

## 💡 Key Takeaways

**`file` is your compass in this level.**  
Never trust the filename extension — always verify with `file` first.
File extensions are just labels. The magic bytes in the file header
never lie. This is a critical forensics instinct.

**The rename before decompress pattern.**  
Most decompression tools require the correct extension to work.
The workflow is always: `file` → identify → `mv` → rename →
decompress → repeat. Skipping the rename causes tool errors.

**Compression layers are real in the wild.**  
Malware, data exfiltration payloads, and CTF challenges all use
layered compression to obfuscate content. The methodology you used
here — identify, rename, decompress, repeat — is genuine forensics
workflow used by real security analysts.

**Working in `/tmp` is a habit, not a workaround.**  
On shared systems you rarely have write permissions in your home
directory. `/tmp` is always writable. Get used to staging your work there.

## 📸 Evidence
![Bandit Level 12 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/f9075dc12adc1f458ce72a4e9cb5a12f2bc8a61a/bandit%20level%2012.png)
![Bandit Level 12 Solution](https://github.com/Darshan-Ga/Linux_lab/blob/f9075dc12adc1f458ce72a4e9cb5a12f2bc8a61a/bandit%20level%2012(2).png)
