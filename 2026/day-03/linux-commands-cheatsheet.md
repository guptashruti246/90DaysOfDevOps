````md
# Linux Commands Cheat Sheet

## 1. File System Commands

### Check current directory
```bash
pwd
```
Shows the current working directory.

### List files and folders
```bash
ls -l
```
Lists files with permissions, owner, and size.

### Show hidden files
```bash
ls -la
```
Lists all files including hidden files.

### Change directory
```bash
cd /path
```
Moves to a different directory.

### Create a directory
```bash
mkdir test
```
Creates a new folder.

### Create an empty file
```bash
touch file.txt
```
Creates a new file.

### Copy files
```bash
cp source.txt backup.txt
```
Copies a file.

### Move or rename file
```bash
mv old.txt new.txt
```
Moves or renames a file.

### Delete file
```bash
rm file.txt
```
Removes a file.

### Delete folder
```bash
rm -r foldername
```
Deletes a directory and contents.

### View file content
```bash
cat file.txt
```
Displays file contents.

### Read large files
```bash
less file.txt
```
Views large files page by page.

### Search text inside file
```bash
grep "error" logfile.log
```
Finds matching text inside files.

---

## 2. Process Management Commands

### View running processes
```bash
ps -ef
```
Shows all running processes.

### Live process monitoring
```bash
top
```
Displays CPU and memory usage.

### Search for process
```bash
ps -ef | grep nginx
```
Finds a specific process.

### Kill process by PID
```bash
kill <PID>
```
Stops a running process.

### Force kill process
```bash
kill -9 <PID>
```
Forcefully terminates a process.

### Check service status
```bash
systemctl status nginx
```
Checks service health.

### Start service
```bash
systemctl start nginx
```
Starts a service.

### Restart service
```bash
systemctl restart nginx
```
Restarts a service.

### Stop service
```bash
systemctl stop nginx
```
Stops a service.

### View logs
```bash
journalctl -xe
```
Shows system logs and errors.

---

## 3. Networking Troubleshooting Commands

### Check IP address
```bash
ip addr
```
Displays network interfaces and IP addresses.

### Test connectivity
```bash
ping google.com
```
Checks if a host is reachable.

### DNS lookup
```bash
dig google.com
```
Checks DNS resolution.

### Test website/API connectivity
```bash
curl https://google.com
```
Tests network access to a URL.

### Check listening ports
```bash
ss -tulnp
```
Shows open ports and services.

### Test remote connection
```bash
ssh user@server-ip
```
Connects to a remote server.

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
ping
ip addr
dig
curl
```
````
