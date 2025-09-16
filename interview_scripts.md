Absolutely! I’ll provide you **ready-to-use Bash scripts** for each of your requested tasks. I’ll categorize them as **Basic**, **Intermediate**, and **Advanced**. Each script will be simple, efficient, and production-friendly.

---

## 🔹 Basic Bash Scripting

### 1. Print numbers from 1 to 100

```bash
#!/bin/bash
for i in {1..100}; do
  echo $i
done
```

---

### 2. Check if a number is even or odd

```bash
#!/bin/bash
read -p "Enter a number: " num
if (( num % 2 == 0 )); then
  echo "$num is even"
else
  echo "$num is odd"
fi
```

---

### 3. Check if a file exists and display its size

```bash
#!/bin/bash
read -p "Enter file path: " file
if [ -f "$file" ]; then
  size=$(du -h "$file" | cut -f1)
  echo "File exists. Size: $size"
else
  echo "File does not exist"
fi
```

---

### 4. Backup a given directory

```bash
#!/bin/bash
read -p "Enter directory to backup: " dir
read -p "Enter backup destination: " dest

if [ -d "$dir" ]; then
  timestamp=$(date +"%Y%m%d_%H%M%S")
  backup_file="$dest/$(basename $dir)_backup_$timestamp.tar.gz"
  tar -czf "$backup_file" "$dir"
  echo "Backup created at $backup_file"
else
  echo "Directory does not exist"
fi
```

---

### 5. Print current date and time in YYYY-MM-DD HH\:MM\:SS

```bash
#!/bin/bash
date +"%Y-%m-%d %H:%M:%S"
```

---

## 🔹 Intermediate Bash Scripting

### 1. Monitor CPU and memory usage and alert

```bash
#!/bin/bash
CPU_THRESHOLD=80
MEM_THRESHOLD=90

CPU=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}' | cut -d. -f1)
MEM=$(free | awk '/Mem/ {printf "%.0f", $3/$2 * 100}')

echo "CPU Usage: $CPU%, Memory Usage: $MEM%"

if [ "$CPU" -gt "$CPU_THRESHOLD" ] || [ "$MEM" -gt "$MEM_THRESHOLD" ]; then
  echo "Alert! High usage detected."
fi
```

---

### 2. Top 5 processes consuming the most memory

```bash
#!/bin/bash
echo "Top 5 memory-consuming processes:"
ps aux --sort=-%mem | head -n 6
```

---

### 3. Check if a service is running and restart if not

```bash
#!/bin/bash
SERVICE="nginx"

if systemctl is-active --quiet $SERVICE; then
  echo "$SERVICE is running"
else
  echo "$SERVICE is not running, restarting..."
  sudo systemctl restart $SERVICE
fi
```

---

### 4. Clean up log files older than 30 days

```bash
#!/bin/bash
LOG_DIR="/var/log"
find "$LOG_DIR" -type f -name "*.log" -mtime +30 -exec rm -f {} \;
echo "Old log files deleted"
```

---

### 5. Check disk usage of `/` partition

```bash
#!/bin/bash
THRESHOLD=80
USAGE=$(df / | awk 'NR==2 {print $5}' | sed 's/%//')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
  echo "Warning! Root partition usage is $USAGE%"
fi
```

---

## 🔹 Advanced / DevOps-Oriented Bash Scripting

### 1. Count "ERROR" occurrences in a log file

```bash
#!/bin/bash
read -p "Enter log file path: " log
if [ -f "$log" ]; then
  count=$(grep -c "ERROR" "$log")
  echo "ERROR found $count times"
else
  echo "Log file does not exist"
fi
```

---

### 2. Fetch AWS EC2 instance IDs and store in a file

```bash
#!/bin/bash
output_file="ec2_instances.txt"
aws ec2 describe-instances --query "Reservations[*].Instances[*].InstanceId" --output text > "$output_file"
echo "Instance IDs saved to $output_file"
```

---

### 3. Check health of multiple URLs

```bash
#!/bin/bash
read -p "Enter file with URLs: " file

while read -r url; do
  status=$(curl -o /dev/null -s -w "%{http_code}" "$url")
  echo "$url : $status"
done < "$file"
```

---

### 4. Deploy a Docker container

```bash
#!/bin/bash
read -p "Enter Docker image (e.g., nginx:latest): " image
read -p "Enter container name: " cname

docker run -d --name "$cname" -p 80:80 "$image"
echo "Container $cname deployed with image $image"
```

---

### 5. Pull latest changes in multiple Git repositories

```bash
#!/bin/bash
read -p "Enter file with repo paths: " file

while read -r repo; do
  if [ -d "$repo/.git" ]; then
    echo "Updating $repo"
    git -C "$repo" pull
  else
    echo "$repo is not a Git repository"
  fi
done < "$file"
```

---

If you want, I can **combine all these scripts into a single “Bash DevOps Toolkit” script** where you can select the task interactively and run it.

Do you want me to do that?
