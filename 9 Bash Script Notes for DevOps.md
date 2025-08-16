Got it 👍 You want **DevOps-focused notes for Bash scripting**, in point form — something you can quickly revise before interviews or while working. Here’s a concise but **comprehensive cheat-sheet style notes list**:

---

# 📝 Bash Script Notes for DevOps

## 1. Basics

* **Shebang** → First line defines interpreter

  ```bash
  #!/bin/bash
  ```
* **Make script executable** → `chmod +x script.sh`
* **Run script** → `./script.sh` or `bash script.sh`

---

## 2. Variables

* Define: `NAME="DevOps"`
* Access: `echo $NAME`
* Command substitution:

  ```bash
  DATE=$(date)
  HOSTNAME=$(hostname)
  ```

---

## 3. Input / Output

* Read input:

  ```bash
  read -p "Enter name: " USER
  echo "Hello $USER"
  ```
* Arguments: `$0` (script name), `$1 $2 ...` (args), `$@` (all args), `$#` (count)

---

## 4. Conditionals

* If statement:

  ```bash
  if [ -f /etc/passwd ]; then
    echo "File exists"
  fi
  ```
* Common checks:

  * `-f file` → file exists
  * `-d dir` → directory exists
  * `-z str` → empty string
  * `-n str` → non-empty string

---

## 5. Loops

* For loop:

  ```bash
  for i in {1..5}; do
    echo "Number $i"
  done
  ```
* While loop:

  ```bash
  while read line; do
    echo $line
  done < file.txt
  ```

---

## 6. Functions

```bash
my_func() {
  echo "Hello $1"
}
my_func DevOps
```

---

## 7. Error Handling

* Exit script: `exit 1`
* Status of last command: `$?` (0=success, non-zero=failure)
* Stop on error: `set -e`
* Debug mode: `set -x`

---

## 8. Useful DevOps Commands

* Disk usage: `df -h`, `du -sh`
* Process check: `ps aux | grep service`
* Network: `netstat -tulnp`, `ss -ltnp`, `curl`, `wget`
* Logs: `tail -f /var/log/syslog`

---

## 9. File Operations

```bash
cp file1 file2
mv file1 file2
rm file.txt
find / -name "*.log"
grep "ERROR" logfile
```

---

## 10. Automation in DevOps

* **Health check scripts** (CPU, memory, disk)
* **Service restart** scripts

  ```bash
  systemctl restart nginx
  ```
* **Log monitoring** with `tail -f`
* **Backup scripts** using `tar`, `rsync`
* **CI/CD** → Bash often used in Jenkins, GitHub Actions, GitLab CI

---

## 11. Advanced Topics

* Arrays:

  ```bash
  arr=("dev" "staging" "prod")
  echo ${arr[1]}
  ```
* Case statement:

  ```bash
  case $1 in
    start) echo "Starting..." ;;
    stop) echo "Stopping..." ;;
    *) echo "Usage: $0 {start|stop}" ;;
  esac
  ```
* Cron jobs → Automate tasks

  ```bash
  crontab -e
  0 2 * * * /path/to/backup.sh
  ```

---

✅ With these points, you can handle **interview questions + real-world DevOps scripting tasks**.

Would you like me to also create a **ready-to-use DevOps Bash script examples pack** (like *health check, backup, log rotation, deployment script*) so you can practice?
