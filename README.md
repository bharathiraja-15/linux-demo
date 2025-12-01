Here is **Level 1 – Basic (Foundational Linux Skills)** explained **STEP-BY-STEP**,
``
1️⃣ Set up users & groups
2️⃣ Manage directory permissions
3️⃣ Install packages (git, nginx, java)
4️⃣ Check system info (CPU, Memory, Disk)

---

# 🟩 **LEVEL 1 – BASIC (FOUNDATIONAL SKILLS)**

## ✅ **1. Create Users and Groups for Dev Team**

### ✔ Step 1: Create a group (example: devteam)

```
sudo groupadd devteam
```

### ✔ Step 2: Add users to the system

```
sudo useradd -m alice
sudo useradd -m bob
sudo useradd -m charlie
```

### ✔ Step 3: Set password for each user

```
sudo passwd alice
sudo passwd bob
sudo passwd charlie
```

### ✔ Step 4: Add users to the devteam group

```
sudo usermod -aG devteam alice
sudo usermod -aG devteam bob
sudo usermod -aG devteam charlie
```

### ✔ Step 5: Confirm group membership

```
groups alice
groups bob
```

---

## ✅ **2. Manage Permissions for Project Directory**

### ✔ Step 1: Create a project folder

```
sudo mkdir -p /project/app1
```

### ✔ Step 2: Change owner to devteam group

```
sudo chown -R :devteam /project/app1
```

### ✔ Step 3: Give read, write, execute permissions to group

```
sudo chmod -R 770 /project/app1
```

### ✔ Step 4: Set group inheritance (important)

This ensures **new files** created inside the folder automatically belong to the group.

```
sudo chmod g+s /project/app1
```

### ✔ Step 5: Verify

```
ls -ld /project/app1
```

Expected:

```
drwxrws---  devteam devteam
```

---

## ✅ **3. Install Required Packages (Git, Nginx, Java)**

### ✔ Update package list

```
sudo apt update
```

### ✔ Install Git

```
sudo apt install -y git
```

Check:

```
git --version
```

### ✔ Install Nginx (Web Server)

```
sudo apt install -y nginx
```

Start + Enable:

```
sudo systemctl start nginx
sudo systemctl enable nginx
```

### ✔ Install Java (OpenJDK 11)

```
sudo apt install -y openjdk-11-jdk
```

Check:

```
java -version
```

---

## ✅ **4. Check System Information (Memory, CPU, Disk)**

### ✔ Check CPU info

```
lscpu
```

### ✔ Check Memory

```
free -h
```

### ✔ Check Disk usage

```
df -h
```

### ✔ Check OS Version

```
cat /etc/os-release
```

### ✔ Check running processes

```
top
```

---

# 🎯 **RESULT**

After completing Level-1:
```
✔ Users created
✔ Groups assigned
✔ Permissions set
✔ Packages installed
✔ System info checked

```
```
Here is **Level 2 – Intermediate (Daily DevOps Tasks)** written in a **clean, precise, professional format** for your **README.md**.
This is optimized for GitHub, interviews, and DevOps portfolio.

```
---

# 🟨 **Level 2 – Intermediate (Daily DevOps Tasks)**

## ✅ **1. Automate Backups Using Cron**

Automate scheduled backups for important application directories.

### **Steps:**

1. Create a backup script:

   ```bash
   /usr/local/bin/app_backup.sh
   ```
2. Add commands to archive project directory:

   ```bash
   tar -czf /backup/app-$(date +%F).tar.gz /project/app1
   ```
3. Make the script executable:

   ```bash
   chmod +x /usr/local/bin/app_backup.sh
   ```
4. Schedule daily backup at 1 AM:

   ```
   crontab -e
   ```

   Add:

   ```
   0 1 * * * /usr/local/bin/app_backup.sh
   ```

---

## ✅ **2. Shell Scripts for Daily Operations**

Create utility scripts used by DevOps team for automation and troubleshooting.

### **a) Log Cleanup Script**

Removes logs older than 7 days.

```bash
find /var/log -type f -mtime +7 -delete
```

### **b) Service Restart Script**

Automatically restarts services that are down.

```bash
systemctl restart nginx
systemctl restart ssh
```

### **c) Health Check Script**

Checks CPU load, memory, disk, and service status.

```bash
uptime
free -h
df -h
systemctl status nginx
```

---

## ✅ **3. Manage Logs Under `/var/log`**

Ensure logs don’t grow too large and rotate properly.

### **Tasks:**

* Check log sizes:

  ```bash
  du -sh /var/log/*
  ```
* Clear old logs:

  ```bash
  sudo truncate -s 0 /var/log/syslog
  ```
* Archive rotated logs:

  ```bash
  gzip /var/log/*.log
  ```

---

## ✅ **4. Monitor System Performance & Troubleshoot**

Daily monitoring of server performance and service health.

### **Commands used:**

* CPU/Load:

  ```
  top
  uptime
  ```
* Memory:

  ```
  free -h
  ```
* Disk usage:

  ```
  df -h
  ```
* Running services:

  ```
  systemctl status <service>
  ```
* Network issues:

  ```
  netstat -tulnp
  ```
* Process issues:

  ```
  ps aux --sort=-%mem
  ```

---

# 🎯 **Summary**

Level 2 covers essential daily DevOps responsibilities:

✔ Automated backups
✔ Log cleanup & management
✔ Service restart automation
✔ Health check scripts
✔ Monitoring CPU, RAM, disk, services
✔ Log management under `/var/log`

This ensures your Linux server is stable, healthy, and ready for production.

---

```
Here is **Level 3 – Advanced (Production-Ready Linux Admin)**
perfect for your GitHub **README.md**.
```
---

# 🟥 **Level 3 – Advanced (Production-Ready Linux Administration)**

## ✅ **1. Create a Custom systemd Service for Your Application**

Use **systemd** to manage your application like a real production service.

### **Steps:**

1. Create a service file:

   ```bash
   sudo nano /etc/systemd/system/myapp.service
   ```
2. Add configuration:

   ```ini
   [Unit]
   Description=My Application Service
   After=network.target

   [Service]
   ExecStart=/usr/local/bin/myapp.sh
   Restart=always
   User=ubuntu

   [Install]
   WantedBy=multi-user.target
   ```
3. Reload systemd:

   ```bash
   sudo systemctl daemon-reload
   ```
4. Start and enable service:

   ```bash
   sudo systemctl start myapp
   sudo systemctl enable myapp
   ```
5. Check status:

   ```bash
   systemctl status myapp
   ```

---

## ✅ **2. SSH Hardening for Security**

Strengthen security by limiting SSH access.

### **Steps:**

1. Edit SSH config:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
2. Apply security changes:

   * Disable root login:

     ```
     PermitRootLogin no
     ```
   * Disable password authentication:

     ```
     PasswordAuthentication no
     ```
   * Change SSH port (example 2222):

     ```
     Port 2222
     ```
3. Restart SSH:

   ```bash
   sudo systemctl restart ssh
   ```
4. Use key-based authentication for secure login.

---

## ✅ **3. LVM Setup for Storage Scaling**

Use Logical Volume Manager to expand storage without downtime.

### **Steps:**

1. Check available disks:

   ```bash
   lsblk
   ```
2. Create Physical Volume:

   ```bash
   sudo pvcreate /dev/sdb
   ```
3. Create Volume Group:

   ```bash
   sudo vgcreate myvg /dev/sdb
   ```
4. Create Logical Volume:

   ```bash
   sudo lvcreate -L 10G -n mylv myvg
   ```
5. Format and mount:

   ```bash
   sudo mkfs.ext4 /dev/myvg/mylv
   sudo mount /dev/myvg/mylv /data
   ```
6. Extend storage anytime:

   ```bash
   sudo lvextend -L +5G /dev/myvg/mylv
   sudo resize2fs /dev/myvg/mylv
   ```

---

## ✅ **4. Configure Firewall Rules**

Secure the server with firewall policies.

### **Using UFW (Ubuntu):**

1. Allow SSH:

   ```bash
   sudo ufw allow 2222/tcp
   ```
2. Allow HTTP/HTTPS:

   ```bash
   sudo ufw allow 80
   sudo ufw allow 443
   ```
3. Enable firewall:

   ```bash
   sudo ufw enable
   ```

### **Using firewalld (CentOS):**

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```

---

## ✅ **5. Implement logrotate for Application Logs**

Rotate log files to prevent disk from filling up.

### **Steps:**

1. Create logrotate config:

   ```bash
   sudo nano /etc/logrotate.d/myapp
   ```
2. Add rules:

   ```
   /var/log/myapp/*.log {
       daily
       rotate 7
       compress
       missingok
       notifempty
   }
   ```
3. Test:

   ```bash
   sudo logrotate -d /etc/logrotate.conf
   ```

---

# 🎯 **Summary (Version 2.0)**

Level 3 focuses on **production-grade Linux administration**, ensuring performance, security, and scalability:

✔ Custom systemd services
✔ SSH security hardening
✔ LVM storage scaling
✔ Firewall rule management
✔ Logrotate for log lifecycle

These tasks reflect **real DevOps engineer responsibilities** in production environments.

---


