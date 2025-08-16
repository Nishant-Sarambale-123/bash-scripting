Perfect 👍 now let’s cover **Conditionals in Bash** with detailed notes, interview Q\&A, and scenarios.

---

# 📝 Bash Scripting Basics – **Conditionals**

## 1. **If Statement**

Basic syntax:

```bash
if [ condition ]; then
  commands
fi
```

Example:

```bash
if [ -f /etc/passwd ]; then
  echo "File exists"
fi
```

---

## 2. **If-Else Statement**

```bash
if [ condition ]; then
  echo "True block"
else
  echo "False block"
fi
```

---

## 3. **If-Elif-Else**

```bash
if [ condition1 ]; then
  echo "Condition 1 true"
elif [ condition2 ]; then
  echo "Condition 2 true"
else
  echo "All conditions false"
fi
```

---

## 4. **Common File Checks**

| Expression | Meaning                    |
| ---------- | -------------------------- |
| `-f file`  | File exists (regular file) |
| `-d dir`   | Directory exists           |
| `-e path`  | File or directory exists   |
| `-r file`  | File is readable           |
| `-w file`  | File is writable           |
| `-x file`  | File is executable         |

---

## 5. **String Checks**

| Expression     | Meaning               |
| -------------- | --------------------- |
| `-z str`       | String is empty       |
| `-n str`       | String is non-empty   |
| `str1 = str2`  | Strings are equal     |
| `str1 != str2` | Strings are not equal |

---

## 6. **Integer Checks**

| Expression | Meaning          |
| ---------- | ---------------- |
| `-eq`      | equal            |
| `-ne`      | not equal        |
| `-gt`      | greater than     |
| `-lt`      | less than        |
| `-ge`      | greater or equal |
| `-le`      | less or equal    |

Example:

```bash
if [ $1 -gt 10 ]; then
  echo "Number is greater than 10"
fi
```

---

## 7. **Logical Operators**

* **AND (`&&` or `-a`)**

  ```bash
  if [ -f file ] && [ -r file ]; then
    echo "File exists and is readable"
  fi
  ```
* **OR (`||` or `-o`)**

  ```bash
  if [ -d dir ] || [ -f file ]; then
    echo "Directory or file exists"
  fi
  ```

---

# 🔹 Interview Q\&A on Conditionals

### **Q1. What is the difference between `[ ]` and `[[ ]]` in Bash?**

**A:**

* `[ ]` → POSIX test command, works in all shells.
* `[[ ]]` → Bash-specific, supports regex and advanced conditions.
  Example:

```bash
if [[ $str == a* ]]; then   # pattern matching
  echo "Starts with a"
fi
```

---

### **Q2. How do you check if a variable is empty in Bash?**

**A:**

```bash
if [ -z "$VAR" ]; then
  echo "Empty"
fi
```

---

### **Q3. How do you check if a directory exists before creating it?**

**A:**

```bash
if [ ! -d /mydir ]; then
  mkdir /mydir
fi
```

---

### **Q4. How do you combine multiple conditions in Bash?**

**A:**
Use `&&` for AND, `||` for OR.

```bash
if [ -f file ] && [ -x file ]; then
  echo "Executable file exists"
fi
```

---

### **Q5. Why should we quote variables inside `[ ]` in conditionals?**

**A:** To avoid errors when variable is empty or contains spaces.

```bash
if [ -z "$VAR" ]; then ...   # Safe
```

---

# 🔹 Scenario Questions

### **Scenario 1:**

Write a script that checks if `/etc/passwd` exists and is readable.

```bash
#!/bin/bash
if [ -f /etc/passwd ] && [ -r /etc/passwd ]; then
  echo "File exists and is readable"
else
  echo "File missing or not readable"
fi
```

---

### **Scenario 2:**

Script to check if a user entered string is empty.

```bash
#!/bin/bash
read -p "Enter name: " NAME
if [ -z "$NAME" ]; then
  echo "No name entered"
else
  echo "Hello $NAME"
fi
```

---

### **Scenario 3:**

Check if number passed as argument is greater than 100.

```bash
#!/bin/bash
if [ $1 -gt 100 ]; then
  echo "Number is greater than 100"
else
  echo "Number is less or equal to 100"
fi
```

---

### **Scenario 4:**

Check if a directory exists; if not, create it.

```bash
#!/bin/bash
DIR="/tmp/testdir"
if [ ! -d "$DIR" ]; then
  mkdir "$DIR"
  echo "Directory created"
else
  echo "Directory already exists"
fi
```

---

✅ **Summary (Quick Revision):**

* **File checks** → `-f`, `-d`, `-r`, `-w`, `-x`
* **String checks** → `-z`, `-n`, `=`, `!=`
* **Integer checks** → `-eq`, `-ne`, `-gt`, `-lt`, `-ge`, `-le`
* **Logical ops** → `&&`, `||`, `!`

---

Would you like me to also prepare a **flowchart-style cheatsheet for conditionals** (visual decision-making: file → dir → string → number checks) so you can revise quickly before interviews?
