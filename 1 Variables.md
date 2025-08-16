Perfect 👍 let’s go deep into **Bash variables** with detailed notes + interview/scenario style Q\&A.

---

# 📝 Bash Scripting Basics – **Variables**

## 1. **Defining a Variable**

* Syntax:

  ```bash
  NAME="DevOps"
  ```
* **Rules:**

  * No spaces around `=`
    ✅ `NAME="DevOps"`
    ❌ `NAME = "DevOps"`
  * Variable names should be **UPPERCASE** (by convention).
  * Can contain letters, numbers, `_`, but **not start with a number**.
    ✅ `USER_NAME="nishant"`
    ❌ `1NAME="wrong"`

---

## 2. **Accessing a Variable**

* Use `$` before the variable name:

  ```bash
  echo $NAME
  ```
* Output:

  ```
  DevOps
  ```

👉 Best practice → wrap in braces `{}` to avoid ambiguity:

```bash
echo ${NAME}_Project
```

Without braces, shell may misread it.

---

## 3. **Command Substitution**

* Run a command and store its result in a variable:

  ```bash
  DATE=$(date)
  HOSTNAME=$(hostname)
  ```
* Now you can use them:

  ```bash
  echo "Today is $DATE"
  echo "Running on $HOSTNAME"
  ```

---

## 4. **Types of Variables**

### a) **User-defined variables**

Created by you in scripts:

```bash
GREETING="Hello DevOps!"
```

### b) **Environment variables**

System-defined and inherited by processes (PATH, HOME, USER, etc.):

```bash
echo $PATH
echo $USER
```

### c) **Special variables**

Bash provides built-in ones:

* `$0` → script name
* `$1, $2 …` → arguments to script
* `$#` → number of arguments
* `$?` → exit status of last command
* `$$` → process ID of script

---

## 5. **Readonly Variables**

Once defined, cannot be modified:

```bash
PI=3.14
readonly PI
PI=22/7   # Error
```

---

## 6. **Unset Variable**

Remove a variable definition:

```bash
unset NAME
```

---

# 🔹 Interview Q\&A on Variables

### **Q1. What is the difference between local, environment, and special variables?**

**A:**

* Local/user-defined → set in script/session.
* Environment → available system-wide for child processes.
* Special → provided by Bash for script handling (`$0`, `$?`, `$#` etc.).

---

### **Q2. How do you assign command output to a variable in Bash?**

**A:** Using command substitution:

```bash
VAR=$(command)
```

Example:

```bash
DATE=$(date)
```

---

### **Q3. Why should we use `${VAR}` instead of `$VAR` sometimes?**

**A:** To avoid ambiguity when appending text:

```bash
NAME="DevOps"
echo "${NAME}_Project"   # Correct
echo "$NAME_Project"     # Wrong, looks for variable "NAME_Project"
```

---

### **Q4. What’s the difference between single quotes `' '` and double quotes `" "` in variable usage?**

**A:**

* `' '` → literal, variables not expanded.
* `" "` → variables expanded.
  Example:

```bash
echo 'Hello $NAME'   # Output: Hello $NAME
echo "Hello $NAME"   # Output: Hello DevOps
```

---

### **Q5. What is `$?` in shell scripting?**

**A:** `$?` stores the **exit status** of the last executed command.

* `0` → success
* non-zero → failure

---

# 🔹 Scenario Questions

### **Scenario 1:**

You set:

```bash
NAME=DevOps Engineer
```

and run:

```bash
echo $NAME
```

👉 Output:

```
DevOps
```

**Why?** Because `Engineer` is treated as another command/word.
**Fix:** Use quotes:

```bash
NAME="DevOps Engineer"
```

---

### **Scenario 2:**

You want to create a log file with today’s date in its name.

```bash
LOGFILE="log_$(date +%Y-%m-%d).txt"
echo "Hello DevOps" > $LOGFILE
```

👉 File created: `log_2025-08-16.txt`

---

### **Scenario 3:**

You need to pass arguments to a script and print them.

```bash
#!/bin/bash
echo "Script name: $0"
echo "First arg: $1"
echo "Second arg: $2"
echo "Total args: $#"
```

Run:

```bash
./myscript.sh DevOps Docker
```

Output:

```
Script name: ./myscript.sh
First arg: DevOps
Second arg: Docker
Total args: 2
```

---

✅ **Summary (Quick Revision):**

* Define: `VAR="value"`
* Access: `$VAR` or `${VAR}`
* Command substitution: `VAR=$(command)`
* Types: user-defined, environment, special
* Important specials: `$0`, `$1`, `$#`, `$?`, `$$`

---

Would you like me to also prepare a **side-by-side table of "most useful Bash variables in DevOps"** (like `$0`, `$1`, `$?`, `$#`, etc. with examples) so you can revise quickly before interviews?
