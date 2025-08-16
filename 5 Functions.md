Great 👍 let’s now go step by step into **Functions in Bash** with detailed notes, interview questions, and DevOps-style scenarios.

---

# 📝 Bash Scripting Basics – **Functions**

A **function** is a reusable block of code that you can call multiple times within a script.

---

## 1. **Defining a Function**

### Syntax 1:

```bash
my_func() {
  echo "Hello $1"
}
```

### Syntax 2:

```bash
function my_func {
  echo "Hello $1"
}
```

👉 Both are valid in Bash.

---

## 2. **Calling a Function**

```bash
my_func DevOps
```

Output:

```
Hello DevOps
```

---

## 3. **Function Parameters**

* `$1`, `$2`, … → Function arguments.
* `$@` → All arguments.
* `$#` → Number of arguments.

Example:

```bash
greet() {
  echo "Hello $1, Welcome to $2"
}
greet Nishant DevOps
```

Output:

```
Hello Nishant, Welcome to DevOps
```

---

## 4. **Return Values**

* In Bash, `return` gives an **exit status (0 = success, non-zero = error)**.
* To return actual data, use **echo** and capture it.

Example (exit code):

```bash
check_file() {
  if [ -f "$1" ]; then
    return 0
  else
    return 1
  fi
}
check_file /etc/passwd
echo $?   # Prints 0 if exists, 1 otherwise
```

Example (return data with echo):

```bash
get_date() {
  echo $(date +%Y-%m-%d)
}
today=$(get_date)
echo "Today is $today"
```

---

## 5. **Local Variables in Functions**

By default, variables inside functions are **global**.
Use `local` to limit scope:

```bash
my_func() {
  local name="DevOps"
  echo "Inside function: $name"
}
my_func
echo "Outside function: $name"   # empty
```

---

# 🔹 Interview Q\&A on Functions

### **Q1. What’s the difference between `return` and `echo` in Bash functions?**

**A:**

* `return` → gives exit code (0 success, non-zero error).
* `echo` → outputs data (to be captured with command substitution).

---

### **Q2. Can Bash functions have default arguments?**

**A:** No, but you can simulate it:

```bash
greet() {
  name=${1:-User}
  echo "Hello $name"
}
greet         # Hello User
greet Nishant # Hello Nishant
```

---

### **Q3. How do you make variables inside a function not affect the global scope?**

**A:** Use the `local` keyword.

---

### **Q4. How to pass all arguments from a function to another command?**

**A:**

```bash
my_func() {
  echo "Arguments: $@"
}
my_func arg1 arg2 arg3
```

---

### **Q5. Can functions be recursive in Bash?**

**A:** Yes, but recursion is not efficient in Bash. Example:

```bash
factorial() {
  if [ $1 -le 1 ]; then
    echo 1
  else
    local temp=$(( $1 - 1 ))
    local result=$(factorial $temp)
    echo $(( $1 * result ))
  fi
}
factorial 5   # Output: 120
```

---

# 🔹 Scenario-Based Examples

### **Scenario 1: Check if a service is running**

```bash
check_service() {
  if systemctl is-active --quiet "$1"; then
    echo "$1 is running"
  else
    echo "$1 is not running"
  fi
}
check_service sshd
```

---

### **Scenario 2: Function to create backup**

```bash
backup_file() {
  cp "$1" "$1.bak"
  echo "Backup created: $1.bak"
}
backup_file /etc/passwd
```

---

### **Scenario 3: Deploy function (Reusable in CI/CD)**

```bash
deploy_app() {
  echo "Pulling latest code..."
  git pull
  echo "Building app..."
  mvn clean package -DskipTests
  echo "Deploying..."
  kubectl apply -f k8s/
}
deploy_app
```

---

### **Scenario 4: Retry command using function**

```bash
retry_cmd() {
  local retries=$1
  shift
  for ((i=1; i<=retries; i++)); do
    "$@" && return 0
    echo "Attempt $i failed, retrying..."
    sleep 2
  done
  return 1
}
retry_cmd 3 curl -s http://example.com
```

---

✅ **Summary (Quick Revision):**

* Functions = reusable code blocks.
* Arguments → `$1`, `$@`, `$#`.
* `return` = exit code, `echo` = data.
* Use `local` for scope.
* Useful in **DevOps automation (deploy, backup, monitoring, retries)**.

---

Do you want me to also prepare a **list of 5 must-know real DevOps functions** (like service check, log monitor, retry, backup, deploy) that you can quickly recall in interviews?
