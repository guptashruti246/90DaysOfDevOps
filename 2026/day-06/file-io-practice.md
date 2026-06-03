# Day 06 – Linux Fundamentals: Read and Write Text Files

## Objective

Practice basic Linux file read and write operations using fundamental commands.

---

## 1. Create a file

Command:

```bash
touch notes.txt
```

Purpose:

Creates an empty file named `notes.txt`.

---

## 2. Write text into file using `>`

Command:

```bash
echo "Linux is the foundation of DevOps." > notes.txt
```

Purpose:

Writes text into the file.

`>` overwrites old content and writes new content.

---

## 3. Append text using `>>`

Command:

```bash
echo "Reading logs helps in troubleshooting." >> notes.txt
```

Purpose:

Adds new text to the existing file.

`>>` appends content without removing previous lines.

---

## 4. Write and display using `tee`

Command:

```bash
echo "Practice builds Linux confidence." | tee -a notes.txt
```

Purpose:

Displays text on the screen and writes it to the file at the same time.

`-a` means append.

---

## 5. Read full file

Command:

```bash
cat notes.txt
```

Purpose:

Displays complete file content.

---

## 6. Read first few lines

Command:

```bash
head -n 2 notes.txt
```

Purpose:

Displays the first 2 lines of the file.

---

## 7. Read last few lines

Command:

```bash
tail -n 2 notes.txt
```

Purpose:

Displays the last 2 lines of the file.

---

## Sample File Content

```text
Linux is the foundation of DevOps.
Reading logs helps in troubleshooting.
Practice builds Linux confidence.
systemctl manages Linux services.
Logs are stored in /var/log.
The /etc directory stores configs.
The /tmp directory stores temporary files.
cat reads full file contents.
head shows first lines of a file.
tail shows last lines of a file.
```

## Key Learnings

* `touch` creates files
* `>` overwrites file content
* `>>` appends content
* `cat` reads full file
* `head` reads first lines
* `tail` reads last lines
* `tee` writes and displays output together
