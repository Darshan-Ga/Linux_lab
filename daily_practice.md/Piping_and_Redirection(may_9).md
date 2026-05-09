# 🐧 Daily Linux Practice: Piping and Redirection

**Focus:** Terminal history extraction and file creation.

## Command Executed
```bash
history | grep "cd" > my_history.txt
```
## Concept Breakdown

* **history:** Retrieves the list of previously executed terminal commands.

* **| (Pipe):** Takes the output of the history command and feeds it directly into the next tool.

* **grep "cd":** Filters the incoming data to only show lines containing the "cd" (change directory) command.

* **> (Output Redirection):** Takes the filtered results and permanently saves them into a new file named my_history.txt.

## Objective

Building daily muscle memory for log parsing, data extraction, and system investigation techniques used in Cloud Security.

![image alt](https://github.com/Darshan-Ga/Linux_lab/blob/280997bf128f3a481d2fe319dd03565da9aaf822/daily_practice.md/%7B91B000AC-FDFF-46A8-8D46-4A7987F7E765%7D.png)
