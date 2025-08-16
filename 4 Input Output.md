Perfect 👍 you’re moving systematically! Let’s go deep into **Input/Output in Bash** with **detailed notes, interview questions, and scenarios**.

---

# 📝 Bash Scripting Basics – **Input / Output**

## 1. **Reading User Input**

* Use the `read` command to take input from the user.
  Example:

```bash
read -p "Enter name: " USER
echo "Hello $USER"
```

* **Explanation:**

  * `-p` → prompt message.
  * Input is stored in variable `USER`.
  * Then printed with `echo`.

👉 Example Run:

```
Enter name: Nishant
Hello Nishant
```

---

## 2. **Script Arguments**

When you run a script, you can pass values as arguments.

Example script (`args.sh`):

```bash
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"
```

Run:

```bash
./args.sh DevOps Docker
```

Output:

```
Script name: ./args.sh
First argument: DevOps
Second argument: Docker
All arguments: DevOps Docker
Number of arguments: 2
```

---

## 3. **Special Argument Variables**

| Variable     | Meaning                       |
| ------------ | ----------------------------- |
| `$0`         | Script name                   |
| `$1`, `$2` … | First, second, etc. argument  |
| `$@`         | All arguments (individually)  |
| `$*`         | All arguments (as one string) |
| `$#`         | Number of arguments           |
| `$$`         | PID (process ID) of script    |
| `$?`         | Exit status of last command   |

---

## 4. **Output**

* `echo` → print output to screen.
* `printf` → formatted output (more control than echo).

Example:

```bash
printf "Name: %s\nAge: %d\n" "Nishant" 25
```

Output:

```
Name: Nishant
Age: 25
```

---

# 🔹 Interview Q\&A on Input/Output

### **Q1. How do you take input from a user in Bash?**

**A:** Using `read` command. Example:

```bash
read -p "Enter your name: " NAME
```

---

### **Q2. What’s the difference between `$@` and `$*`?**

**A:**

* `$@` → treats arguments as **separate words** (good for loops).
* `$*` → treats all arguments as **a single string**.

Example:

```bash
for arg in "$@"; do echo $arg; done
```

Prints each argument separately.
But with `$*`, it prints them as one combined string.

---

### **Q3. How can you get the number of arguments passed to a script?**

**A:** Using `$#`.

---

### **Q4. If a script has `read` input and also takes arguments, which one is preferred in automation?**

**A:** Arguments are preferred for automation (CI/CD pipelines) because they can be passed non-interactively. `read` is mostly for manual scripts.

---

### **Q5. What is `$?` and why is it useful in scripting?**

**A:** `$?` stores exit status of last command (`0 = success, non-zero = failure`). Useful for error handling in automation.

---

# 🔹 Scenario Questions

### **Scenario 1:**

Script should ask user for a filename and then print line count.

```bash
#!/bin/bash
read -p "Enter filename: " FILE
if [ -f "$FILE" ]; then
  echo "Line count: $(wc -l < $FILE)"
else
  echo "File not found!"
fi
```

---

### **Scenario 2:**

Script should take 2 numbers as arguments and add them.

```bash
#!/bin/bash
NUM1=$1
NUM2=$2
SUM=$((NUM1 + NUM2))
echo "Sum = $SUM"
```

Run:

```bash
./sum.sh 10 20
```

Output:

```
Sum = 30
```

---

### **Scenario 3:**

Loop through all arguments passed to script.

```bash
#!/bin/bash
for arg in "$@"; do
  echo "Argument: $arg"
done
```

Run:

```bash
./loop.sh DevOps Docker Kubernetes
```

Output:

```
Argument: DevOps
Argument: Docker
Argument: Kubernetes
```

---

✅ **Summary (Quick Revision):**

* `read -p "Prompt" VAR` → read user input.
* `$0` → script name.
* `$1, $2…` → arguments.
* `$@` → all arguments (separately).
* `$*` → all arguments (as one string).
* `$#` → number of arguments.

---

Would you like me to also prepare a **comparison table of Input methods** (User input via `read` vs Arguments via `$1,$2`) → when to use which in DevOps?
