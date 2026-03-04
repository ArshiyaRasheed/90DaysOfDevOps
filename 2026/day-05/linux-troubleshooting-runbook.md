# Day 05 – Linux Troubleshooting Runbook

## Target Service / Process
Service: sshd  
Purpose: Handles remote SSH connections

---

## 1️⃣ Environment Basics

### Command 1
uname -a
<img width="825" height="26" alt="image" src="https://github.com/user-attachments/assets/9767852b-f705-4cad-b787-3904e3964d6a" />

Observation: 
→ Kernel version 6.14 running on Ubuntu-based system.

### command 2
cat /etc/os-release
<img width="601" height="179" alt="image" src="https://github.com/user-attachments/assets/ccb993e4-683b-461f-8664-5c8a3a6d791e" />
observation:
ubuntu 24.04.3 LTS

---

## 2️⃣ Filesystem Sanity Check

### Command 3
mkdir /tmp/runbook-demo
<img width="474" height="146" alt="image" src="https://github.com/user-attachments/assets/918f7d9d-089a-48d1-b11d-7e53a63d1a44" />

Observation:
Directory created successfully.

### Command 4
cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo
<img width="637" height="38" alt="image" src="https://github.com/user-attachments/assets/921b98dd-1009-4c5d-af70-50975335e658" />

Observation:
File copied successfully. Permissions intact.
→ Filesystem is writable and behaving normally.

-----

## 3️⃣ Snapshot: CPU & Memory

### Command 5
ps -o pid,pcpu,pmem,comm -C sshd
<img width="400" height="68" alt="image" src="https://github.com/user-attachments/assets/1adc44f4-6a71-4f5d-a2a8-4d666e4f23ff" />

Observation:
PID   %CPU   %MEM   COMMAND  
151650  0.0    0.9  sshd  

→ sshd is consuming minimal CPU and memory.

### Command 6
free -h
<img width="540" height="48" alt="image" src="https://github.com/user-attachments/assets/0b209bf7-b3f7-4c72-9bf9-a2ff19860701" />

Observation:
Total RAM: 914Mi 
Used: 374Mi 
Available: 540Mi 

----

## 4️⃣ Snapshot: Disk & IO

### Command 7
df -h
<img width="460" height="137" alt="image" src="https://github.com/user-attachments/assets/ee8d1414-f5e1-413e-9ef6-26a58c677b9e" />

Observation:
Root partition 38% used.  
→ No disk space issue.

### Command 8
du -sh /var/log
<img width="356" height="25" alt="image" src="https://github.com/user-attachments/assets/49f75530-6bd4-47fb-bd20-52b458bd04d6" />

Observation:
Log directory size: 52MB  
→ Logs not excessively large.

----

## 5️⃣ Snapshot: Network

### Command 9
ss -tulpn | grep ssh
<img width="371" height="29" alt="image" src="https://github.com/user-attachments/assets/c3d4e2a1-5547-45e5-a6e7-f8dd9b493fa6" />

### Command 10
curl -I localhost
<img width="613" height="23" alt="image" src="https://github.com/user-attachments/assets/e7bf793b-4def-48b8-a74a-e2e3a8b79ee8" />

Observation:
Connection refused  
→ Expected since SSH is not an HTTP service.

---

## 6️⃣ Logs Reviewed

### Command 11
journalctl -u ssh -n 50
<img width="933" height="209" alt="image" src="https://github.com/user-attachments/assets/513d6482-49ff-460a-bbfe-52323095fb49" />

Observation:
We see error  
Login attempts fails

### Command 12
tail -n 50 /var/log/auth.log
<img width="930" height="241" alt="image" src="https://github.com/user-attachments/assets/643eb98b-0780-40a2-bf48-8eed17e81c35" />

Observation:
Normal authentication logs.  
Repeated failed login attempts.

---

## Quick Findings

- SSH service is running normally.
- CPU and memory usage are minimal.
- Disk space sufficient.
- No abnormal log entries.
- Network port 22 is listening properly.

System health: ✅ Stable

---

## If This Worsens (Next Steps)

1. Check failed login spikes:
   journalctl -u ssh --since "1 hour ago"

2. Restart service if unresponsive:
   sudo systemctl restart ssh

3. Deep inspection:
   sudo strace -p <pid>
   or enable debug mode in sshd_config

---

## Lessons Learned

- Always capture system state before restarting services.
- Check logs before assuming resource exhaustion.
- Verify network listener before investigating firewall.

  






