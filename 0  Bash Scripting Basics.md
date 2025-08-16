Perfect 👍
If you’re preparing Bash scripting basics for **DevOps interviews**, you should know not only the commands but also how to **explain them in interviews** and answer **scenario-based questions**.

Here’s a **complete package: notes + interview Q\&A + scenario questions**.

---

# 📝 Bash Scripting Basics + Interview Prep

## 1. **Shebang (`#!`)**

* First line in a script (`#!/bin/bash`).
* Tells OS which interpreter to use.
* Without Shebang → system’s default shell is used (may cause errors).

---

## 2. **Making Script Executable**

```bash
chmod +x script.sh
```

* `+x` gives execute permission.
* `ls -l` confirms permissions.

---

## 3. **Running a Script**

* **Executable mode (Shebang used):**

  ```bash
  ./script.sh
  ```
* **Explicit interpreter:**

  ```bash
  bash script.sh
  ```
* Difference:

  * `./script.sh` → relies on Shebang.
  * `bash script.sh` → forces Bash.

---

# 🔹 Interview Questions & Answers

### **Q1. What is a Shebang and why is it important?**

**A:** Shebang (`#!`) is the first line of a script that defines which interpreter executes the file. For example, `#!/bin/bash` ensures the script runs in Bash, not in `/bin/sh` (which may not support some Bash features).

---

### **Q2. Difference between `./script.sh` and `bash script.sh`?**

**A:**

* `./script.sh` → needs execute permission, uses the interpreter defined in Shebang.
* `bash script.sh` → doesn’t need execute permission, always runs with Bash, ignores Shebang.

---

### **Q3. Why do we need `chmod +x` before running a script?**

**A:** By default, a file doesn’t have execute permission. `chmod +x` gives execute rights so the system can treat it as a program.

---

### **Q4. If Shebang is missing, what happens?**

**A:** The script runs with the system’s default shell (`/bin/sh` in most Linux systems). This may break the script if it uses Bash-specific syntax.

---

### **Q5. How do you run a script that is not in your current directory?**

**A:** Use either an absolute path (`/home/user/script.sh`) or relative path (`../script.sh`). If the script is in `$PATH`, you can run it just by its name.

---

### **Q6. What happens if you write `sh script.sh` for a Bash script?**

**A:** It will execute using `sh` (POSIX shell). If the script has Bash-only syntax (like arrays, `[[ ]]`, or `function` keyword), it may fail.

---

# 🔹 Scenario-Based Questions

### **Scenario 1:**

You wrote a script `deploy.sh` with `#!/bin/bash` at the top, but when you run `./deploy.sh`, you get:

```
bash: ./deploy.sh: Permission denied
```

👉 **Answer:** The script doesn’t have execute permissions. Fix it with:

```bash
chmod +x deploy.sh
./deploy.sh
```

---

### **Scenario 2:**

You run a script with:

```bash
bash script.sh
```

It runs fine. But with:

```bash
./script.sh
```

you get errors.
👉 **Answer:** The Shebang might be wrong (e.g., `#!/bin/sh`). With `bash script.sh` you forced Bash, so it worked. Need to fix Shebang to `#!/bin/bash`.

---

### **Scenario 3:**

You copied a script from Windows to Linux and tried to run it, but got:

```
bad interpreter: No such file or directory
```

👉 **Answer:** Windows uses `\r\n` (CRLF) line endings, Linux expects `\n`. Fix by:

```bash
dos2unix script.sh
```

---

### **Scenario 4:**

You want to run a script globally (from anywhere) without typing `./`.
👉 **Answer:** Move it to a directory in your `$PATH`, e.g.:

```bash
sudo mv script.sh /usr/local/bin/
```

Then run it directly:

```bash
script.sh
```

---

### **Scenario 5:**

You need a script to run with **different interpreters**. How would you handle?
👉 **Answer:** Either:

* Use correct Shebang for each interpreter (`#!/bin/bash`, `#!/usr/bin/env python3`, etc.),
* Or explicitly run with interpreter (`python3 script.py`, `bash script.sh`).

---

✅ This covers **theory, interview Q\&A, and real troubleshooting scenarios**.

Would you like me to also prepare a **mini "scenario practice sheet"** (like 10 short problems to solve in Bash basics) so you can self-test before interviews?
