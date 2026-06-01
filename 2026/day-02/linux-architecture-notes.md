# Linux Architecture, Processes, and systemd

## 1. Core Components of Linux

### Kernel

* The **core of Linux** that interacts directly with hardware.
* Responsible for:

  * CPU management
  * Memory management
  * Device management
  * Process management
* Acts as a bridge between hardware and applications.

### User Space

* Area where users and applications run.
* Commands like `ls`, `top`, `vim`, and applications run here.
* Cannot directly access hardware; requests go through the kernel.

### Init / systemd

* First process started during Linux boot.
* Has **PID 1**.
* Responsible for:

  * Starting services
  * Managing processes
  * Handling boot process

Examples of services:

* nginx
* docker
* sshd
* mariadb

---

## 2. Process Management in Linux

A **process** is a running instance of a program.

Example:
When a command is executed:

```bash id="ic9slg"
ls
```

Linux creates a process to run it.

### Process Creation

* A parent process creates a child process.
* Every process has a unique **PID (Process ID)**.
* To view running processes:

```bash id="eqn2vb"
ps -ef
```

### Process States

#### Running (R)

* Process is actively using CPU.

#### Sleeping (S)

* Waiting for input or resources.
* Most processes remain in this state.

#### Stopped (T)

* Process paused manually.

#### Zombie (Z)

* Process finished execution but still exists in process table.

---

## 3. What systemd Does

`systemd` is Linux's **service manager**.

It helps:

* Start services during boot
* Stop/restart services
* Monitor failed services
* Manage logs

### Common Commands

```bash id="pqbrmp"
systemctl status nginx
systemctl start docker
systemctl stop mariadb
systemctl restart sshd
```

### Why systemd Matters

Understanding `systemd` helps:

* Debug crashed services
* Troubleshoot production issues
* Check logs and restart services quickly

---

## 4. 5 Linux Commands Used Daily

### Check running processes

```bash id="8h2j4m"
ps -ef
```

### Monitor CPU and memory

```bash id="6iyxry"
top
```

### Check service status

```bash id="k0s4l8"
systemctl status <service>
```

### View system logs

```bash id="j0cfyy"
journalctl -xe
```

### Kill a process

```bash id="vduzux"
kill <PID>
```

---

## Summary

Linux works using the **kernel, user space, and systemd**. Understanding processes and services helps troubleshoot issues faster and is essential for DevOps and system administration.
