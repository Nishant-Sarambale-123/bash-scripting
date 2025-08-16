Perfect 👌 now let’s cover **Loops in Bash** with **detailed notes, interview-style questions, and scenarios**.

---

# 📝 Bash Scripting Basics – **Loops**

Loops are used to execute a block of code repeatedly until a condition is met.

---

## 1. **For Loop**

### Syntax 1: Sequence

```bash
for i in {1..5}; do
  echo "Number $i"
done
```

Output:

```
Number 1
Number 2
Number 3
Number 4
Number 5
```

---

### Syntax 2: List of items

```bash
for fruit in apple banana mango; do
  echo "Fruit: $fruit"
done
```

---

### Syntax 3: Using `C-style for loop`

```bash
for (( i=1; i<=5; i++ )); do
  echo "Count: $i"
done
```

---

## 2. **While Loop**

* Runs as long as the condition is **true**.

Example:

```bash
i=1
while [ $i -le 5 ]; do
  echo "Number $i"
  ((i++))
done
```

---

## 3. **While Loop with File Input**

```bash
while read line; do
  echo $line
done < file.txt
```

👉 Reads `file.txt` line by line and prints each line.

---

## 4. **Until Loop**

* Opposite of `while` → runs until condition becomes **true**.

```bash
i=1
until [ $i -gt 5 ]; do
  echo "Number $i"
  ((i++))
done
```

---

## 5. **Loop Control**

* **break** → exit loop immediately.
* **continue** → skip current iteration and move to next.

Example:

```bash
for i in {1..5}; do
  if [ $i -eq 3 ]; then
    continue
  fi
  echo "Number $i"
done
```

👉 Prints numbers 1,2,4,5 (skips 3).

---

# 🔹 Interview Q\&A on Loops

### **Q1. What’s the difference between `while` and `until` loops in Bash?**

**A:**

* `while` → runs while condition is **true**.
* `until` → runs while condition is **false** (stops when true).

---

### **Q2. How can you iterate over all files in a directory using Bash?**

**A:**

```bash
for file in /path/to/dir/*; do
  echo "File: $file"
done
```

---

### **Q3. How do you read a file line by line in Bash?**

**A:**

```bash
while read line; do
  echo $line
done < filename
```

---

### **Q4. How can you loop through script arguments?**

**A:**

```bash
for arg in "$@"; do
  echo "Argument: $arg"
done
```

---

### **Q5. How can you stop a loop after finding a match in a file?**

**A:**
Use `break`:

```bash
while read line; do
  if [[ $line == "STOP" ]]; then
    break
  fi
  echo $line
done < file.txt
```

---

# 🔹 Scenario Questions

### **Scenario 1:** Print numbers 1–10, but skip 5.

```bash
for i in {1..10}; do
  if [ $i -eq 5 ]; then
    continue
  fi
  echo $i
done
```

---

### **Scenario 2:** Read all usernames from `/etc/passwd` and print them.

```bash
while IFS=: read -r user _; do
  echo "User: $user"
done < /etc/passwd
```

---

### **Scenario 3:** Retry a command until it succeeds.

```bash
until ping -c1 google.com &>/dev/null; do
  echo "Retrying..."
  sleep 2
done
echo "Network is up!"
```

---

### **Scenario 4:** Create 5 log files.

```bash
for i in {1..5}; do
  touch "log_$i.txt"
done
```

---

✅ **Summary (Quick Revision):**

* **for loop** → iterate over list, sequence, or C-style counter.
* **while loop** → run while condition true.
* **until loop** → run until condition true.
* **read loop** → process file line by line.
* **break / continue** → control flow.

---

Would you like me to also prepare a **comparison table (For vs While vs Until)** so you can quickly revise which loop to use in which DevOps scenario (e.g., retrying, file processing, iterations)?
