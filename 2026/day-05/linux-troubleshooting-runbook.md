# Linux Troubleshooting Runbook – CPU, Memory, Disk, Network & Logs

## Target Service / Process

### Service Chosen: `sshd` (SSH Service)

**Why this service?**

* SSH is used to remotely access Linux servers.
* If SSH stops working, administrators cannot log into the server.
* It is one of the most important Linux services for system management.

---

# 1. Environment Basics

## Check Kernel and System Information

**Command:**

```bash
uname -a
```

**Purpose:**

* Displays Linux kernel version.
* Shows architecture and hostname.

**Observation:**

* Verified the Linux kernel version and confirmed system architecture.

---

## Check Operating System Information

**Command:**

```bash
cat /etc/os-release
```

**Purpose:**

* Shows Linux distribution details.

**Observation:**

* Confirmed OS name and version.

---

# 2. Filesystem Sanity Check

## Create Temporary Test Directory

**Command:**

```bash
mkdir /tmp/runbook-demo
```

**Purpose:**

* Creates a temporary folder for testing file operations.

**Observation:**

* Directory created successfully.

---

## Copy and Verify File

**Command:**

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

**Purpose:**

* Copies a system file for testing.
* Verifies file permissions and successful copy.

**Observation:**

* File copied successfully and visible in the directory.

---

# 3. Snapshot: CPU & Memory Health

## Monitor Live System Resources

**Command:**

```bash
top
```

**Purpose:**

* Displays live CPU, memory, and process activity.

**What I Checked:**

* CPU usage percentage
* Memory consumption
* Running processes

**Observation:**

* CPU usage was stable.
* No abnormal memory spikes found.
* No process consuming excessive CPU.

---

## Check Memory Usage

**Command:**

```bash
free -h
```

**Purpose:**

* Shows RAM and swap memory usage.

**Observation:**

* Enough free memory available.
* No memory pressure observed.

---

## Check SSH Process Resource Usage

**Command:**

```bash
ps -o pid,pcpu,pmem,comm -C sshd
```

**Purpose:**

* Displays PID, CPU usage, memory usage, and process name for SSH service.

**Observation:**

* SSH process was consuming minimal CPU and memory.

---

# 4. Snapshot: Disk & IO Health

## Check Disk Usage

**Command:**

```bash
df -h
```

**Purpose:**

* Displays disk usage in human-readable format.

**What I Checked:**

* Root partition usage
* Available storage

**Observation:**

* Disk usage was within acceptable range.
* No filesystem was critically full.

---

## Check Log Directory Size

**Command:**

```bash
du -sh /var/log
```

**Purpose:**

* Checks size of log directory.

**Observation:**

* Log storage usage was reasonable.
* No unusually large logs found.

---

## Check System Performance

**Command:**

```bash
vmstat 2 5
```

**Purpose:**

* Monitors CPU, memory, and system performance.

**Observation:**

* System performance appeared healthy.
* No heavy CPU wait times observed.

---

# 5. Snapshot: Network Health

## Check Open Ports and Listening Services

**Command:**

```bash
ss -tulpn
```

**Purpose:**

* Displays listening ports and services.

**What I Checked:**

* Verified SSH port availability.

**Observation:**

* SSH service listening on port `22`.

---

## Test Local Connectivity

**Command:**

```bash
curl -I localhost
```

**Purpose:**

* Tests whether localhost responds.

**Observation:**

* Successfully received response headers.

---

## Verify SSH Process

**Command:**

```bash
pgrep sshd
```

**Purpose:**

* Finds PID of SSH service.

**Observation:**

* SSH process was running successfully.

---

# 6. Logs Reviewed

## Review SSH Logs

**Command:**

```bash
journalctl -u sshd -n 50
```

**Purpose:**

* Displays last 50 logs for SSH service.

**What I Checked:**

* Failed login attempts
* Service restart errors
* Authentication issues

**Observation:**

* No recent critical SSH errors found.

---

## Review Recent System Logs

**Command:**

```bash
tail -n 50 /var/log/messages
```

**Purpose:**

* Shows recent system activity logs.

**Observation:**

* Normal system activity observed.
* No major warnings or failures found.

---

# 7. Quick Findings

### Service Health

* SSH service was active and running normally.

### CPU & Memory

* No unusual CPU spikes.
* Memory usage remained healthy.

### Disk Health

* Disk space was sufficient.
* Logs were not consuming excessive storage.

### Network

* SSH port was open and listening.
* Localhost connectivity worked correctly.

### Logs

* No recent SSH failures or critical warnings found.

---

# 8. If This Worsens (Next Steps)

## 1. Restart SSH Service

If SSH becomes unresponsive:

```bash
systemctl restart sshd
```

---

## 2. Check Detailed Error Logs

If login failures continue:

```bash
journalctl -u sshd -xe
```

---

## 3. Investigate Resource Issues

If system becomes slow:

```bash
top
free -h
ps -ef | grep sshd
```

---

## 4. Verify Network Connectivity

If SSH access fails:

```bash
ss -tulpn
ping localhost
```

---

## 5. Escalation Step

If issue still persists:

* Collect logs
* Document observations
* Escalate to infrastructure or Linux support team
