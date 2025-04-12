# 🧠 Day 2 – Basic Linux Commands

## 📝 Summary

On Day 2 of DevOps training, we were introduced to essential Linux commands. These are foundational for working with servers, especially in cloud and DevOps environments where Linux is the dominant operating system.

---

## 📂 Directory & File Management

| Command               | Description                                         |
|------------------------|-----------------------------------------------------|
| `pwd`                 | Displays the present working directory              |
| `ls`                  | Lists files and directories                         |
| `ls -l`               | Long listing format with details                    |
| `ls -a`               | Shows hidden files                                  |
| `cd <directory>`      | Changes to the specified directory                  |
| `cd ..`               | Moves one directory up                              |
| `mkdir <folder>`      | Creates a new directory                             |
| `rmdir <folder>`      | Deletes an empty directory                          |
| `touch <file>`        | Creates an empty file                               |
| `rm <file>`           | Deletes a file                                      |
| `rm -r <folder>`      | Deletes a folder and its contents                   |
| `mv <src> <dest>`     | Moves or renames files/directories                  |
| `cp <src> <dest>`     | Copies files or directories                         |

---

## 📄 File Viewing & Editing

| Command               | Description                                         |
|------------------------|-----------------------------------------------------|
| `cat <file>`          | Displays file content                              |
| `more <file>` / `less <file>` | Views file content page by page         |
| `head -n 10 <file>`   | Displays the first 10 lines of a file              |
| `tail -n 10 <file>`   | Displays the last 10 lines of a file               |
| `nano <file>`         | Opens file in nano text editor                     |
| `vi <file>`           | Opens file in vi editor                            |
| `echo "text" > file`  | Writes text to file (overwrite)                    |
| `echo "text" >> file` | Appends text to a file                             |

---

## 📦 File Permissions & Ownership

| Command                        | Description                                 |
|--------------------------------|---------------------------------------------|
| `chmod +x <file>`              | Makes a file executable                     |
| `chmod 755 <file>`             | Sets read/write/execute permissions         |
| `chown user:user <file>`       | Changes ownership of file                   |
| `ls -l`                        | View file permissions                       |

---

## 📑 System Info & Monitoring

| Command               | Description                                         |
|------------------------|-----------------------------------------------------|
| `clear`               | Clears terminal screen                             |
| `history`             | Shows command history                              |
| `whoami`              | Prints current user name                           |
| `uname -a`            | Displays detailed system information               |
| `uptime`              | Shows system uptime                                |
| `top`                 | Displays real-time running processes               |
| `htop`                | Interactive version of top (if installed)          |
| `free -h`             | Displays memory usage in human-readable format     |
| `df -h`               | Shows disk usage                                   |

---

## 🔎 Searching & Filtering

| Command                           | Description                               |
|----------------------------------|-------------------------------------------|
| `grep "pattern" <file>`          | Searches for text in a file               |
| `find . -name "*.yml"`           | Finds files by name pattern               |
| `wc -l <file>`                   | Counts lines in a file                    |
| `sort <file>`                    | Sorts content of a file                   |
| `cut -d ":" -f 1 <file>`         | Cuts a column based on delimiter          |

---

## 🌐 Networking & Internet

| Command               | Description                                         |
|------------------------|-----------------------------------------------------|
| `ping google.com`     | Checks internet connectivity                       |
| `curl <url>`          | Fetches data from a web URL                        |
| `wget <url>`          | Downloads files from the internet                  |
| `ifconfig` / `ip a`   | Displays IP address and interfaces                 |
| `netstat -tulpn`      | Lists listening ports and associated processes     |

---

## 🔄 Process Management

| Command               | Description                                         |
|------------------------|-----------------------------------------------------|
| `ps aux`              | Lists running processes                            |
| `kill <PID>`          | Kills a process by PID                             |
| `kill -9 <PID>`       | Forcefully kills a process                         |
| `bg` / `fg`           | Move jobs to background or foreground              |

---

## 📦 Package Management (Ubuntu/Debian)

| Command                       | Description                                 |
|-------------------------------|---------------------------------------------|
| `sudo apt update`             | Updates list of available packages          |
| `sudo apt upgrade`            | Installs the latest versions of packages    |
| `sudo apt install <package>`  | Installs a package                          |
| `sudo apt remove <package>`   | Removes a package                           |

---

## 🔐 User Management

| Command               | Description                                         |
|------------------------|-----------------------------------------------------|
| `adduser <username>`  | Adds a new user                                    |
| `passwd <username>`   | Sets/changing password                             |
| `who`                 | Lists logged-in users                              |
| `su - <user>`         | Switches to another user                           |

---

## ✅ Outcome

Gained hands-on experience using basic and advanced Linux commands for:

- Navigating and managing the filesystem
- Viewing and editing files
- Handling users, permissions, and packages
- Monitoring system resources
- Managing processes and networking

These commands form the core skill set needed for system administration and DevOps practices. Mastery of the Linux shell is essential for working with Kubernetes, Docker, CI/CD tools, and remote cloud servers.

---
