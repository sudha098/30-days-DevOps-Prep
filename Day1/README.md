
# 🚀 **DAY 1 — Linux Essentials (Strong Foundation)**

Today’s goal: Build strong Linux fundamentals required for senior DevOps/SRE roles.

---

# 🧠 **1. Concepts (Basic → Intermediate)**

### **Understand these deeply:**

### ✔ Filesystem hierarchy

* `/etc` – configs
* `/var/log` – logs
* `/usr/bin` – binaries
* `/opt` – optional apps
* `/srv` – service data

### ✔ Users, Groups & Permissions

* `chmod`, `chown`, `umask`
* ACLs (`getfacl`, `setfacl`)
* Special bits: SUID, SGID, Sticky bit

### ✔ Processes

* PID, PPID
* Process states
* Foreground vs background vs daemon

### ✔ systemd basics

* Units
* service files
* enable/disable/start/stop

### ✔ Shell fundamentals

* redirections
* pipes
* basic scripting patterns

---

# 💻 **2. Hands-On Labs (2 hours)**

Do these step by step on ANY Linux VM (Ubuntu/CentOS).

---

## **LAB 1 — User & Permission Management**

### Create users & groups:

```bash
sudo groupadd devteam
sudo useradd -m -s /bin/bash alice
sudo useradd -m -s /bin/bash bob
sudo usermod -aG devteam alice
sudo usermod -aG devteam bob
```

### Create shared directory:

```bash
sudo mkdir /shared
sudo chgrp devteam /shared
sudo chmod 770 /shared
```

### Add ACL permissions:

```bash
sudo setfacl -m u:alice:rwx /shared
sudo setfacl -m u:bob:r-x /shared
getfacl /shared
```

**Expected result:** bob can read, alice can write.

---

## **LAB 2 — Filesystem Exploration**

Run:

```bash
ls -l /bin /usr/sbin /var/log
du -sh /etc/*
sudo find / -type f -size +100M
```

Learn: size, permissions, discovering files.

---

## **LAB 3 — Process & Service Management**

### Create a sample service:

Create file:
`/etc/systemd/system/myapp.service`

```
[Unit]
Description=My Custom App
After=network.target

[Service]
Type=simple
ExecStart=/usr/bin/sleep infinity

[Install]
WantedBy=multi-user.target
```

Load & start:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now myapp
sudo systemctl status myapp
```

### Kill & restart process:

```bash
ps aux | grep sleep
sudo kill -9 <PID>
```

Check auto-restart behaviour.

---

## **LAB 4 — Logging**

```bash
journalctl -u myapp
journalctl -xe
```

Learn how to navigate logs.

---

# 🏗 **3. Architecture Task (10 min)**

**Design Linux folder structure & access rules for a server hosting:**

* a production backend
* logs accessible to SREs only
* deployments done by CI/CD user
* application configs editable by platform engineers only

Write this in 5–10 bullet points.

---

# 🛠 **4. Troubleshooting Challenge (10 min)**

**A systemd service fails to start with error: “ExecStart not found”.**
Investigate and fix using:

* `journalctl -u servicename`
* check wrong path
* missing permissions
* wrong file format

Write your fix steps.

---

# ❓ **5. Mini Quiz**

1. What does the sticky bit do on a directory?
2. Difference between `chmod 755` and `chmod 775`?
3. What happens when a process is orphaned?
4. Which directory stores persistent system-wide configs?
5. What does `umask` control?

Write your answers — I’ll evaluate.

---

# 🧾 **6. Notes to Memorize Today**

* Linux permissions are the foundation of secure infrastructure
* Systemd is used everywhere: containers, VMs, bare metal
* ACLs override traditional permissions
* `/var/log` is your best friend during incidents
* Always check `journalctl` first for any issue

---
