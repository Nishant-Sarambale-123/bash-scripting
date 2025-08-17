Got it 👍 — You want **DevOps bash scripting coding interview questions with answers and proper explanations**.
I’ll cover from **basic → intermediate → advanced**, along with real-world **DevOps scenarios**.

---

# 📌 DevOps Bash Scripting Coding Questions & Answers

---

## **1. Print numbers from 1 to 10**

👉 *Basic question to test loops*

**Question:** Write a script to print numbers from 1 to 10.

```bash
#!/bin/bash
for i in {1..10}
do
  echo $i
done
```

✅ **Explanation:**

* `{1..10}` → brace expansion in bash.
* `for loop` iterates through numbers 1 to 10.
* Prints each number.

---

## **2. Check if a file exists**

👉 *File handling question*

**Question:** Write a script to check if a file exists or not.

```bash
#!/bin/bash
FILE="/etc/passwd"

if [ -f "$FILE" ]; then
  echo "File $FILE exists."
else
  echo "File $FILE does not exist."
fi
```

✅ **Explanation:**

* `-f` → checks if given path is a regular file.
* Useful in automation (checking config/log files).

---

## **3. Find top 5 memory-consuming processes**

👉 *Real-world monitoring task*

**Question:** Write a script to display the top 5 memory-consuming processes.

```bash
#!/bin/bash
ps -eo pid,comm,%mem --sort=-%mem | head -n 6
```

✅ **Explanation:**

* `ps -eo` → display PID, command, memory usage.
* `--sort=-%mem` → sort by memory descending.
* `head -n 6` → 1 header + 5 processes.

📌 **Scenario in DevOps:** Used for quick health checks in servers/pods.

---

## **4. Disk usage alert script**

👉 *Common DevOps automation*

**Question:** Create a script to check if `/` disk usage is above 80%, and send an alert.

```bash
#!/bin/bash
THRESHOLD=80
USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
  echo "CRITICAL: Disk usage is $USAGE% on /"
else
  echo "OK: Disk usage is $USAGE%"
fi
```

✅ **Explanation:**

* `df -h /` → check root filesystem.
* `awk 'NR==2 {print $5}'` → extract usage column.
* `sed 's/%//'` → remove `%`.
* Condition triggers alert when usage > threshold.

📌 **Scenario:** Common in **cron jobs** for monitoring servers.

---

## **5. Backup script with timestamp**

👉 *Practical DevOps automation*

**Question:** Write a script to backup `/etc` into `/tmp` with a timestamp.

```bash
#!/bin/bash
SRC="/etc"
DEST="/tmp/etc-backup-$(date +%F-%H%M%S).tar.gz"

tar -czf "$DEST" "$SRC"
echo "Backup created at $DEST"
```

✅ **Explanation:**

* `$(date +%F-%H%M%S)` → creates unique filename with date & time.
* `tar -czf` → compress into `.tar.gz`.

📌 **Scenario:** Backup automation in **CI/CD pipelines** or cron jobs.

---

## **6. Extract IP addresses from logs**

👉 *Text processing (very common in interviews)*

**Question:** From `access.log`, extract all unique IP addresses.

```bash
#!/bin/bash
awk '{print $1}' access.log | sort | uniq
```

✅ **Explanation:**

* `awk '{print $1}'` → print first column (IP).
* `sort | uniq` → remove duplicates.

📌 **Scenario:** Useful for analyzing logs (Nginx/Apache).

---

## **7. Script to restart service if down**

👉 *Ops automation scenario*

**Question:** Write a script that checks if `nginx` is running, restart if not.

```bash
#!/bin/bash
SERVICE="nginx"

if ! systemctl is-active --quiet $SERVICE; then
  echo "$SERVICE is down. Restarting..."
  systemctl restart $SERVICE
else
  echo "$SERVICE is running."
fi
```

✅ **Explanation:**

* `systemctl is-active --quiet` → checks service status.
* `if ! ...` → negation means "if not running".
* Restarts service automatically.

📌 **Scenario:** Auto-healing scripts for servers.

---

## **8. Read user input**

👉 *Interactive question*

**Question:** Write a script that asks user for a filename and checks existence.

```bash
#!/bin/bash
read -p "Enter filename: " FILE

if [ -e "$FILE" ]; then
  echo "$FILE exists."
else
  echo "$FILE does not exist."
fi
```

✅ **Explanation:**

* `read -p` → prompt for input.
* `-e` → checks if file exists (any type).

---

## **9. Monitor CPU usage in a loop**

👉 *Intermediate automation*

**Question:** Write a script to check CPU usage every 5 sec and exit if usage > 80%.

```bash
#!/bin/bash
THRESHOLD=80

while true
do
  USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}')
  USAGE=${USAGE%.*}   # Remove decimal
  
  echo "CPU Usage: $USAGE%"
  
  if [ "$USAGE" -gt "$THRESHOLD" ]; then
    echo "High CPU usage detected: $USAGE%"
    exit 1
  fi
  sleep 5
done
```

✅ **Explanation:**

* `top -bn1` → batch mode output of CPU usage.
* `100 - idle` = usage %.
* Script runs in loop & checks usage.

📌 **Scenario:** Performance monitoring scripts.

---

## **10. Deploy app if new code is found**

👉 *Advanced DevOps pipeline scenario*

**Question:** Write a script to check if new code is pushed to Git repo, then pull and redeploy.

```bash
#!/bin/bash
REPO_DIR="/opt/myapp"

cd $REPO_DIR || exit

git fetch

if [ $(git rev-parse HEAD) != $(git rev-parse @{u}) ]; then
  echo "New changes found. Pulling and redeploying..."
  git pull
  docker-compose down
  docker-compose up -d --build
else
  echo "No new changes."
fi
```

✅ **Explanation:**

* `git fetch` → check remote changes.
* Compare `HEAD` (local) with `@{u}` (upstream).
* If mismatch → pull code, rebuild & restart Docker.

📌 **Scenario:** Automation in **CI/CD deployment pipelines**.

---

🔥 These cover **basic, intermediate, advanced, and real-world DevOps scenarios**.

Do you want me to also prepare a **list of tricky one-liner Bash interview questions** (like string reverse, Fibonacci, factorial, etc.) that interviewers often ask?
