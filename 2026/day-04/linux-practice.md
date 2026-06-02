# Linux Practice – Processes and Services

## 1. Process Checks

### Check Running Processes

**Command:**

```bash
ps -ef | head
```

**Purpose:**

* Shows currently running processes.
* `-e` = all processes
* `-f` = full format output.
* `head` limits output to first few lines.

**Observation:**

* Saw system processes running with different PIDs.

---

### Check Process by Name

**Command:**

```bash
pgrep sshd
```

**Purpose:**

* Finds the PID of a specific process.

**Observation:**

* Returned the PID of the `sshd` service.

---

## 2. Service Checks

### Check SSH Service Status

**Command:**

```bash
systemctl status sshd
```

**Purpose:**

* Checks whether the SSH service is running.

**Observation:**

* Service was active and running.

---

### List Active Services

**Command:**

```bash
systemctl list-units --type=service
```

**Purpose:**

* Displays active system services.

**Observation:**

* Saw services like `sshd`, `cron`, and `NetworkManager`.

---

## 3. Log Checks

### Check SSH Logs

**Command:**

```bash
journalctl -u sshd
```

**Purpose:**

* Displays logs related to the SSH service.

**Observation:**

* Saw login-related logs.

---

### View Recent System Logs

**Command:**

```bash
tail -n 50 /var/log/messages
```

**Purpose:**

* Shows the last 50 lines of system logs.

**Observation:**

* Found service and system activity logs.

---

## 4. Mini Troubleshooting Steps

### Scenario

Verify whether the SSH service is working correctly.

### Steps Followed

**1. Check service status**

```bash
systemctl status sshd
```

**2. Review service logs**

```bash
journalctl -u sshd
```

**3. Confirm process is running**

```bash
pgrep sshd
```

### Result

* SSH service was running correctly with no major errors found.
