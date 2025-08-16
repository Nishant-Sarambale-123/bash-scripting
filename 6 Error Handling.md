Perfect 👍 let’s make **Error Handling in Bash** into a full set of detailed notes with examples, interview Q\&A, and DevOps scenarios.

---

# 📝 Bash Scripting Basics – **Error Handling**

Error handling ensures your script behaves safely when things go wrong.

---

## 1. **Exit Script**

```bash
echo "Something went wrong"
exit 1
```

* `exit 0` → success.
* `exit 1` (or non-zero) → failure.
* Used to stop script execution when a critical failure happens.

---

## 2. **Status of Last Command (`$?`)**

```bash
ls /etc/passwd
echo $?   # 0 if file exists, else non-zero
```

* `$?` holds the exit code of the **last executed command**.
* `0 = success`, `non-zero = failure`.

---

## 3. **Stop Script on First Error (`set -e`)**

```bash
set -e
cp /not/exist /tmp/
echo "This line will not run"
```

* When enabled, the script stops if **any command fails**.
* Useful for CI/CD pipelines where a single failure should break the pipeline.

---

## 4. **Debug Mode (`set -x`)**

```bash
set -x
echo "Debugging this script"
ls /etc/passwd
set +x   # Turn off debugging
```

* Prints each command before executing it (like trace logs).
* Helps find where a script is failing.

---

## 5. **Combining Options**

```bash
set -euo pipefail
```

* `-e` → exit on error.
* `-u` → error on undefined variables.
* `-o pipefail` → catch errors in piped commands.

---

# 🔹 Interview Q\&A

### **Q1. What is the difference between `exit` and `set -e`?**

* `exit` → manually stops the script with a specific exit code.
* `set -e` → automatically stops script on any command failure.

---

### **Q2. How can you debug a shell script?**

* Add `set -x` at the top of the script.
* Or run: `bash -x script.sh`

---

### **Q3. What does `$?` return after running a command?**

* The exit status of the last command (`0 = success, non-zero = error`).

---

### **Q4. Why is `set -euo pipefail` recommended in production scripts?**

* Ensures script fails fast on error.
* Prevents using unset variables.
* Detects errors in pipelines (e.g., `cmd1 | cmd2`).

---

### **Q5. How do you handle errors gracefully instead of exiting immediately?**

* Use conditional checks:

```bash
if ! cp file.txt /tmp/; then
  echo "Copy failed!"
fi
```

* Or use a **trap** to run cleanup:

```bash
trap 'echo "Error occurred. Cleaning up..."; exit 1' ERR
```

---

# 🔹 Scenario-Based Examples

### **Scenario 1: File Backup with Error Check**

```bash
backup_file="/etc/passwd"
dest="/tmp/passwd.bak"

if cp "$backup_file" "$dest"; then
  echo "Backup successful: $dest"
else
  echo "Backup failed!"
  exit 1
fi
```

---

### **Scenario 2: CI/CD Build Script**

```bash
set -e

echo "Building application..."
mvn clean package -DskipTests

echo "Deploying to Kubernetes..."
kubectl apply -f deployment.yaml
```

👉 If build fails, script stops (no bad deployments).

---

### **Scenario 3: Debugging Pipeline**

```bash
set -x
cat file.txt | grep "error" | wc -l
set +x
```

👉 Helps trace which step in the pipeline caused an issue.

---

### **Scenario 4: Retry on Failure**

```bash
retry() {
  for i in {1..3}; do
    "$@" && return 0
    echo "Attempt $i failed, retrying..."
    sleep 2
  done
  echo "All attempts failed!"
  return 1
}
retry curl -s http://example.com
```

---

✅ **Quick Revision (Error Handling in Bash):**

* `exit 1` → stop script manually.
* `$?` → exit status of last command.
* `set -e` → stop on error.
* `set -x` → debug mode.
* `trap` → cleanup on error.
* Best practice → `set -euo pipefail`.

---

Would you like me to also make a **Top 5 DevOps Error Handling Scenarios** (like failed deployments, service crash, log monitoring, missing config, failed backup) that you can directly use in interview prep?
