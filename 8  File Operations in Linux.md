Great 👍 Let’s break **File Operations in Shell Scripting** into detailed **notes + interview Q\&A + scenarios**

---

# 📝 9. File Operations in Linux

File handling is **one of the most common tasks** for DevOps engineers – copying, moving, deleting, searching, and filtering log files.

---

## 🔹 1. Copy File

```bash
cp file1 file2
```

* Copies contents of `file1` to `file2`.
* If `file2` exists → it will be **overwritten**.
* Add `-r` for directories:

```bash
cp -r dir1 dir2
```

---

## 🔹 2. Move / Rename File

```bash
mv file1 file2
```

* Moves `file1` to `file2`.
* If both are in the same directory → effectively a **rename**.

---

## 🔹 3. Remove File

```bash
rm file.txt
```

* Deletes `file.txt`.

* Use with caution ⚠️.

* Delete directory:

```bash
rm -r mydir
```

* Force delete (no confirmation):

```bash
rm -rf mydir
```

---

## 🔹 4. Find Files

```bash
find / -name "*.log"
```

* Searches **recursively** starting from `/`.
* Finds all files ending with `.log`.
* Case-insensitive search:

```bash
find / -iname "*.log"
```

* Limit depth:

```bash
find /var/log -maxdepth 1 -name "*.log"
```

---

## 🔹 5. Search Inside Files (grep)

```bash
grep "ERROR" logfile
```

* Finds lines containing `ERROR`.
* Case-insensitive:

```bash
grep -i "error" logfile
```

* Recursive search in directory:

```bash
grep -r "ERROR" /var/log
```

* Show line numbers:

```bash
grep -n "ERROR" logfile
```

---

# 🔹 Interview Q\&A

### **Q1. What’s the difference between `rm` and `rmdir`?**

* `rm` → deletes files (and directories with `-r`).
* `rmdir` → removes **empty directories only**.

---

### **Q2. How do you find all `.log` files modified in the last 2 days?**

```bash
find /var/log -name "*.log" -mtime -2
```

---

### **Q3. How do you search for a specific error message inside logs?**

```bash
grep "OutOfMemoryError" /var/log/app.log
```

---

### **Q4. Difference between `cp` and `mv`?**

* `cp` → copy file (original remains).
* `mv` → move/rename (original removed).

---

### **Q5. How do you delete all `.tmp` files in `/tmp`?**

```bash
find /tmp -name "*.tmp" -delete
```

---

# 🔹 DevOps Scenarios

### **Scenario 1: Clean Up Old Log Files**

Disk full due to old logs → remove logs older than 7 days:

```bash
find /var/log -name "*.log" -mtime +7 -exec rm -f {} \;
```

---

### **Scenario 2: Search for Errors in CI/CD Pipeline Logs**

```bash
grep -i "failed" /var/lib/jenkins/jobs/myjob/build.log
```

👉 Quickly locate failed stages.

---

### **Scenario 3: Move Config Files During Deployment**

```bash
mv config_new.yaml /etc/myapp/config.yaml
```

👉 Replace old config with new version.

---

### **Scenario 4: Backup Before Editing**

```bash
cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
```

👉 Always keep a backup before changes.

---

### **Scenario 5: Find Large Files Eating Disk**

```bash
find / -type f -size +500M
```

👉 Helps in debugging disk usage issues.

---

✅ **Quick Revision (File Ops):**

* Copy → `cp file1 file2`.
* Move/Rename → `mv file1 file2`.
* Remove → `rm file.txt`, `rm -rf dir`.
* Find files → `find / -name "*.log"`.
* Search inside file → `grep "ERROR" logfile`.

---

Do you want me to also prepare a **cheat sheet of all file operations (with flags & examples)** in a **tabular format** so you can revise quickly before interviews?
