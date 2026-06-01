# Linux Commands Cheat Sheet

## 1. File System Commands

| Command                    | Usage                                    |
| -------------------------- | ---------------------------------------- |
| `pwd`                      | Shows current working directory          |
| `ls -l`                    | Lists files with permissions and details |
| `ls -la`                   | Shows hidden files                       |
| `cd /path`                 | Changes directory                        |
| `mkdir test`               | Creates a new directory                  |
| `touch file.txt`           | Creates an empty file                    |
| `cp source.txt backup.txt` | Copies a file                            |
| `mv old.txt new.txt`       | Moves or renames a file                  |
| `rm file.txt`              | Deletes a file                           |
| `rm -r foldername`         | Deletes a folder and contents            |
| `cat file.txt`             | Displays file content                    |
| `less file.txt`            | Reads large files page by page           |
| `grep "error" logfile.log` | Searches text inside a file              |

---

## 2. Process Management Commands

| Command                   | Usage                         |
| ------------------------- | ----------------------------- |
| `ps -ef`                  | Shows running processes       |
| `top`                     | Monitors CPU and memory usage |
| `ps -ef \| grep nginx`    | Finds a specific process      |
| `kill <PID>`              | Stops a process               |
| `kill -9 <PID>`           | Forcefully kills a process    |
| `systemctl status nginx`  | Checks service status         |
| `systemctl start nginx`   | Starts a service              |
| `systemctl restart nginx` | Restarts a service            |
| `systemctl stop nginx`    | Stops a service               |
| `journalctl -xe`          | Views system logs             |

---

## 3. Networking Troubleshooting Commands

| Command                   | Usage                                   |
| ------------------------- | --------------------------------------- |
| `ip addr`                 | Shows IP addresses and interfaces       |
| `ping google.com`         | Tests connectivity                      |
| `dig google.com`          | Checks DNS resolution                   |
| `curl https://google.com` | Tests website/API connectivity          |
| `ss -tulnp`               | Shows open ports and listening services |
| `ssh user@server-ip`      | Connects to a remote server             |

---

## Quick Troubleshooting Flow

### Service Issue

```bash
systemctl status <service>
journalctl -xe
```

### High CPU / Memory

```bash
top
ps -ef
```

### Network Issue

```bash
ping google.com
ip addr
dig google.com
curl https://google.com
```
