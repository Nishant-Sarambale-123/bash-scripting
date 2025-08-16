Perfect 👍 let’s make this into **DevOps Useful Commands Notes** with details, interview questions, and scenarios.

---

# 📝 Useful DevOps Commands

As a DevOps engineer, you’ll often troubleshoot systems, check resource usage, monitor processes, and debug network issues.

---

## 1. **Disk Usage**

🔹 Check available disk space:

```bash
df -h
```

* `-h` → human-readable (GB/MB).
* Shows **disk partitions** and usage %.

🔹 Check size of a directory:

```bash
du -sh /var/log
```

* `-s` → summary only.
* `-h` → human-readable.

👉 Useful for finding which directory is eating disk.

---

## 2. **Process Check**

🔹 List all processes:

```bash
ps aux
```

* `a` → all users.
* `u` → detailed info (user, CPU, memory).
* `x` → processes without a terminal.

🔹 Find specific process:

```bash
ps aux | grep nginx
```

👉 Helps find running services and PIDs.

---

## 3. **Network Commands**

🔹 Check open ports:

```bash
netstat -tulnp
```

* `t` → TCP.
* `u` → UDP.
* `l` → listening.
* `n` → show numbers (not names).
* `p` → process ID/program.

🔹 Modern replacement:

```bash
ss -ltnp
```

👉 Faster than `netstat`.

🔹 Check connectivity:

```bash
curl -I http://example.com
wget http://example.com
```

* `curl` → test APIs, endpoints.
* `wget` → download files.

---

## 4. **Logs**

🔹 Check system logs in real time:

```bash
tail -f /var/log/syslog
```

* `-f` → follow log as it grows.

🔹 Check application logs:

```bash
tail -f /var/log/nginx/error.log
```

---

# 🔹 Interview Q\&A

### **Q1. Difference between `df` and `du`?**

* `df` → shows disk usage of **file systems/partitions**.
* `du` → shows disk usage of **files/directories**.

---

### **Q2. How do you check which process is using port 8080?**

```bash
netstat -tulnp | grep 8080
# or
ss -ltnp | grep 8080
```

---

### **Q3. How do you troubleshoot a service not running?**

1. Check if process exists: `ps aux | grep service`
2. Check if port is open: `ss -ltnp`
3. Check logs: `tail -f /var/log/service.log`

---

### **Q4. How do you monitor logs in real-time in Linux?**

* Use `tail -f` or `less +F`.

---

### **Q5. When would you use `curl` vs `wget`?**

* `curl` → API testing, sending requests.
* `wget` → downloading files.

---

# 🔹 DevOps Scenarios

### **Scenario 1: Disk Full in CI/CD Pipeline**

```bash
df -h
du -sh /var/lib/docker/*
```

👉 Find which Docker images/volumes are consuming space.

---

### **Scenario 2: Application Not Starting**

```bash
ps aux | grep myapp
ss -ltnp | grep 8080
tail -f /var/log/myapp.log
```

👉 Check if process is running, port is bound, and logs for errors.

---

### **Scenario 3: Debugging Web Server**

```bash
curl -I http://localhost:80
tail -f /var/log/nginx/error.log
```

👉 See if server responds and check error logs.

---

### **Scenario 4: Network Troubleshooting**

```bash
ping google.com
traceroute google.com
curl -I https://api.github.com
```

👉 Verify DNS, routing, and API availability.

---

### **Scenario 5: High CPU Usage**

```bash
top
ps aux --sort=-%cpu | head -5
```

👉 Identify top CPU-hungry processes.

---

✅ **Quick Revision (DevOps Commands):**

* Disk: `df -h`, `du -sh`.
* Processes: `ps aux | grep`.
* Network: `netstat -tulnp`, `ss -ltnp`, `curl`, `wget`.
* Logs: `tail -f file.log`.

---

Would you like me to also create a **one-page cheat sheet (tabular format)** for these commands (with purpose + example), so you can keep it handy for interviews?
