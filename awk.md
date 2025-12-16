Below are **detailed AWK command notes** written in **very simple words**, perfect for **DevOps / Linux interviews and daily usage**.

---

# 📘 AWK Command – Detailed Notes (Simple Words)

## 🔹 What is AWK?

**AWK** is a **text processing tool** in Linux.

👉 It is mainly used to:

* Read a file **line by line**
* **Split each line into columns (fields)**
* Perform **actions** like print, filter, calculate, format output

💡 Very useful for:

* Log analysis
* Reports
* Extracting columns
* Monitoring scripts (DevOps)

---

## 🔹 How AWK Works (Simple Flow)

1. Read **one line**
2. Split the line into **fields**
3. Apply **condition**
4. Perform **action**
5. Move to **next line**

---

## 🔹 Basic AWK Syntax

```bash
awk 'pattern { action }' file_name
```

Example:

```bash
awk '{print}' file.txt
```

✔ Prints every line (same as `cat`)

---

## 🔹 Fields in AWK (Very Important)

| Symbol | Meaning                     |
| ------ | --------------------------- |
| `$0`   | Entire line                 |
| `$1`   | First column                |
| `$2`   | Second column               |
| `$NF`  | Last column                 |
| `NF`   | Number of columns           |
| `NR`   | Line number                 |
| `FNR`  | Line number in current file |

---

## 🔹 Example File (`data.txt`)

```text
101 Ravi 50000
102 Amit 60000
103 Sita 55000
```

---

## 🔹 Print Specific Columns

### Print first column

```bash
awk '{print $1}' data.txt
```

Output:

```text
101
102
103
```

---

### Print multiple columns

```bash
awk '{print $1, $2}' data.txt
```

---

### Print last column

```bash
awk '{print $NF}' data.txt
```

---

## 🔹 Print with Custom Message

```bash
awk '{print "ID:", $1, "Name:", $2}' data.txt
```

---

## 🔹 Conditions in AWK

### Print lines where salary > 55000

```bash
awk '$3 > 55000 {print}' data.txt
```

---

### Print only matching text

```bash
awk '$2 == "Amit" {print}' data.txt
```

---

### Not equal

```bash
awk '$3 != 50000 {print}' data.txt
```

---

## 🔹 Using NR (Line Number)

### Print line number

```bash
awk '{print NR, $0}' data.txt
```

---

### Print only 2nd line

```bash
awk 'NR==2 {print}' data.txt
```

---

## 🔹 Using NF (Number of Fields)

### Print lines with exactly 3 columns

```bash
awk 'NF==3 {print}' data.txt
```

---

## 🔹 BEGIN and END Blocks

### BEGIN (Runs before reading file)

```bash
awk 'BEGIN {print "ID NAME SALARY"} {print}' data.txt
```

---

### END (Runs after file ends)

```bash
awk 'END {print "End of File"}' data.txt
```

---

### BEGIN + END Together

```bash
awk 'BEGIN {print "Start"} {print} END {print "Finish"}' data.txt
```

---

## 🔹 Calculations in AWK

### Add two columns

```bash
awk '{print $1 + $3}' data.txt
```

---

### Total salary

```bash
awk '{sum += $3} END {print sum}' data.txt
```

---

### Average salary

```bash
awk '{sum += $3} END {print sum/NR}' data.txt
```

---

## 🔹 Field Separator (FS)

### Default separator = space

### Use colon `:` as separator

```bash
awk -F: '{print $1}' /etc/passwd
```

---

### Change separator inside script

```bash
awk 'BEGIN{FS=":"} {print $1}' /etc/passwd
```

---

## 🔹 Output Field Separator (OFS)

```bash
awk 'BEGIN{OFS="-"} {print $1,$2}' data.txt
```

---

## 🔹 Pattern Matching (Regex)

### Lines containing "Amit"

```bash
awk '/Amit/ {print}' data.txt
```

---

### Lines starting with 10

```bash
awk '/^10/ {print}' data.txt
```

---

### Lines ending with 000

```bash
awk '/000$/ {print}' data.txt
```

---

## 🔹 If–Else in AWK

```bash
awk '{if($3 > 55000) print $2 " High Salary"; else print $2 " Normal"}' data.txt
```

---

## 🔹 While Loop

```bash
awk '{i=1; while(i<=NF){print $i; i++}}' data.txt
```

---

## 🔹 For Loop

```bash
awk '{for(i=1;i<=NF;i++) print $i}' data.txt
```

---

## 🔹 Built-in Functions

| Function     | Use         |
| ------------ | ----------- |
| `length($0)` | Line length |
| `toupper()`  | Uppercase   |
| `tolower()`  | Lowercase   |
| `substr()`   | Substring   |

Example:

```bash
awk '{print toupper($2)}' data.txt
```

---

## 🔹 AWK with Pipelines (DevOps Use)

### Get 2nd column from ps

```bash
ps -ef | awk '{print $2}'
```

---

### Check disk usage > 80%

```bash
df -h | awk '$5 > 80 {print}'
```

---

## 🔹 AWK vs SED vs CUT

| Tool | Purpose                      |
| ---- | ---------------------------- |
| awk  | Column + logic + calculation |
| sed  | Replace, delete, edit text   |
| cut  | Simple column extraction     |

---

## 🔹 Interview One-Liners

✔ AWK is a **pattern scanning and processing language**
✔ Default field separator is **space**
✔ `$0` means **whole line**
✔ `NR` means **line number**
✔ Best for **logs & reports**

---

## 🔹 Real DevOps Example

```bash
kubectl get pods | awk '{print $1}'
```

---

If you want, I can also provide:

* 📄 **AWK cheat sheet**
* 🎯 **Interview questions**
* 🔁 **Real-time log examples**
* 📝 **Practice exercises**

Just tell me 👍
