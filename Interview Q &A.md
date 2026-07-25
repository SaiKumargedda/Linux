# Linux Advanced Interview Questions & Answers (DevOps – 4+ Years)

---

# Q1. A production application is not accessible. How do you troubleshoot?

### Answer

I follow a layer-by-layer approach instead of randomly checking things.

**Step 1: Check if the service is running**

```bash
systemctl status app
```

**Step 2: Check if the process exists**

```bash
ps -ef | grep java
```

**Step 3: Check if the application is listening on the expected port**

```bash
ss -tulnp
```

**Step 4: Verify locally**

```bash
curl http://localhost:8080/health
```

**Step 5: Check logs**

```bash
journalctl -u app

tail -100 app.log
```

**Step 6: Verify disk, CPU and memory**

```bash
df -h

free -h

top
```

**Step 7: Verify DNS and connectivity**

```bash
nslookup app.company.com

ping app.company.com
```

---

# Q2. Disk usage is 100%. What do you do?

### Answer

```bash
df -h
```

Find large directories

```bash
du -sh /*
```

Find large files

```bash
find / -type f -size +500M
```

Actions

* Remove unnecessary files
* Compress old logs
* Run logrotate if required
* Extend disk if needed

---

# Q3. Disk usage is still 100% even after deleting a huge log file.

### Answer

A running process may still have the deleted file open.

Check

```bash
lsof | grep deleted
```

Restart the application or process holding the file descriptor.

This releases the disk space.

---

# Q4. What is an inode?

### Answer

An inode stores metadata about a file.

It contains

* Owner
* Permissions
* File size
* Timestamps
* Disk block locations

It does **not** store the filename.

Check inode

```bash
ls -li
```

---

# Q5. Disk has free space but you cannot create new files.

### Answer

Most likely **inode exhaustion**.

Check

```bash
df -i
```

If inode usage is 100%, delete small unnecessary files.

---

# Q6. Difference between Hard Link and Soft Link?

### Answer

Hard Link

* Same inode
* Same data
* Survives original file deletion

Soft Link

* Different inode
* Shortcut to original file
* Breaks if original file is deleted

---

# Q7. Difference between kill and kill -9?

### Answer

**kill**

Sends SIGTERM.

Allows graceful shutdown.

Application can clean resources.

**kill -9**

Sends SIGKILL.

Immediate termination.

Cannot be caught or ignored.

---

# Q8. What is a Zombie Process?

### Answer

A zombie process has completed execution, but its parent has not collected its exit status.

Check

```bash
ps -el | grep Z
```

Usually fixed by restarting or terminating the parent process.

---

# Q9. What is an Orphan Process?

### Answer

If the parent process exits before the child, the child becomes an orphan.

The init/systemd process adopts it.

---

# Q10. What is OOM Killer?

### Answer

OOM (Out Of Memory) Killer is a Linux mechanism that terminates processes when the system runs out of memory.

Check

```bash
dmesg | grep -i oom
```

---

# Q11. How do you check high CPU usage?

### Answer

```bash
top
```

or

```bash
ps -eo pid,comm,%cpu --sort=-%cpu | head
```

Identify the process, analyse logs and restart or optimise if necessary.

---

# Q12. How do you check high memory usage?

### Answer

```bash
free -h

top
```

Largest consumers

```bash
ps -eo pid,comm,%mem --sort=-%mem | head
```

---

# Q13. How do you identify which process is using a port?

### Answer

```bash
ss -tulnp
```

Example

```text
LISTEN

*:8080

users:(("java",pid=2456))
```

PID 2456 is using port 8080.

---

# Q14. Difference between curl and ping?

### Answer

**ping**

Checks network connectivity using ICMP.

**curl**

Checks application or web server response using HTTP/HTTPS.

---

# Q15. Difference between nslookup and dig?

### Answer

Both resolve DNS.

**dig**

Provides more detailed DNS information.

**nslookup**

Provides a simpler output.

---

# Q16. Difference between df and du?

### Answer

df

Filesystem usage.

du

Directory or file usage.

---

# Q17. Difference between top and ps?

### Answer

top

Real-time monitoring.

ps

Snapshot of current processes.

---

# Q18. Difference between RPM and YUM?

### Answer

RPM

Installs a package manually.

YUM

Automatically resolves dependencies from repositories.

---

# Q19. Difference between tar and gzip?

### Answer

tar

Archives multiple files.

gzip

Compresses a file.

Usually combined as

```text
backup.tar.gz
```

---

# Q20. What is Log Rotation?

### Answer

Log rotation prevents log files from consuming all disk space.

It

* Renames current log
* Creates new log
* Compresses old logs
* Deletes very old logs

---

# Q21. Is Log Rotation a Backup?

### Answer

No.

Log rotation manages logs locally.

Backups copy logs to another storage location such as another server or cloud storage.

---

# Q22. Difference between SSH and SCP?

### Answer

SSH

Remote login.

SCP

Secure file transfer.

---

# Q23. Difference between find and locate?

### Answer

find

Searches the live filesystem.

locate

Searches an indexed database.

Much faster.

---

# Q24. What does /etc/resolv.conf contain?

### Answer

DNS server configuration.

Example

```text
nameserver 8.8.8.8

nameserver 1.1.1.1
```

Linux uses these servers to resolve hostnames.

---

# Q25. What does systemctl do?

### Answer

Manages services.

Examples

```bash
systemctl status nginx

systemctl restart nginx

systemctl enable nginx
```

---

# Q26. Difference between journalctl and tail?

### Answer

journalctl

Reads logs stored by systemd.

tail

Reads plain text log files.

---

# Q27. What happens when a Linux server becomes slow?

### Answer

Check

```bash
top

free -h

df -h

vmstat

iostat
```

Then analyse logs

```bash
journalctl

tail
```

Finally check the application and network.

---

# Q28. What is a File Descriptor?

### Answer

A file descriptor is a number that Linux assigns to every open file, socket or pipe.

Standard descriptors

* 0 → stdin
* 1 → stdout
* 2 → stderr

Too many open files can cause applications to fail.

Check limits

```bash
ulimit -n
```

---

# Q29. How do you know which ports are open?

### Answer

```bash
ss -tulnp
```

Shows

* Port
* Protocol
* Listening state
* Process
* PID

---

# Q30. Explain your daily Linux activities as a DevOps Engineer.

### Sample Answer

"As part of my daily activities, I connect to Linux servers using SSH, verify application health using systemctl, ps and ss, analyse logs with journalctl and tail, monitor CPU, memory and disk using top, free and df, verify network connectivity with curl, ping and nslookup, perform file transfers using SCP, manage permissions using chmod and chown, and troubleshoot deployment issues in collaboration with application teams."

---

# Frequently Used Commands

```bash
ls
pwd
cd
cat
tail
grep
find
df
du
free
top
ps
ss
systemctl
journalctl
curl
ping
nslookup
dig
tar
gzip
ssh
scp
chmod
chown
```

---

# Interview Tips

* Explain your troubleshooting in a logical order (service → process → port → logs → resources → network → DNS).
* Mention the command and **why** you use it, not just the syntax.
* Use production examples where possible.
* Avoid saying "I directly restart the service." Always mention that you verify logs and identify the root cause first.

This approach demonstrates structured production troubleshooting, which interviewers expect from a DevOps Engineer with 4+ years of experience.
