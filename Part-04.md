# Linux README – Part 4

## (Package Management, SSH, Archives, Environment Variables, Boot Process & Interview Scenarios)

---

# 1. Package Management

Linux packages are used to install, update and remove software.

## RPM (Red Hat Package Manager)

Check installed package

```bash
rpm -q nginx
```

Install package

```bash
rpm -ivh nginx.rpm
```

Remove package

```bash
rpm -e nginx
```

---

## YUM

Used in RHEL/CentOS.

Install

```bash
sudo yum install nginx
```

Update package

```bash
sudo yum update nginx
```

Update all packages

```bash
sudo yum update
```

Remove

```bash
sudo yum remove nginx
```

Search package

```bash
yum search docker
```

---

## DNF

Replacement for YUM in newer RHEL versions.

```bash
sudo dnf install git
```

---

## APT (Ubuntu)

Install

```bash
sudo apt install nginx
```

Update repository

```bash
sudo apt update
```

Upgrade packages

```bash
sudo apt upgrade
```

Remove

```bash
sudo apt remove nginx
```

---

# 2. Environment Variables

Display all

```bash
printenv
```

Display one variable

```bash
echo $HOME
```

Set temporarily

```bash
export APP_ENV=dev
```

Verify

```bash
echo $APP_ENV
```

Permanent

Edit

```bash
~/.bashrc
```

Reload

```bash
source ~/.bashrc
```

---

# 3. SSH

Connect to remote server

```bash
ssh user@192.168.1.20
```

Using key

```bash
ssh -i id_rsa user@server
```

---

# 4. SCP

Copy file to remote server

```bash
scp app.jar user@server:/opt/apps/
```

Copy directory

```bash
scp -r project user@server:/opt/
```

Copy from remote

```bash
scp user@server:/tmp/log.txt .
```

---

# 5. Archive Files (tar)

Create archive

```bash
tar -cvf backup.tar app/
```

Options

* c → Create
* v → Verbose
* f → File

Extract

```bash
tar -xvf backup.tar
```

Compressed archive

```bash
tar -czvf backup.tar.gz app/
```

Extract compressed archive

```bash
tar -xzvf backup.tar.gz
```

---

# 6. gzip

Compress

```bash
gzip app.log
```

Result

```text
app.log.gz
```

Decompress

```bash
gunzip app.log.gz
```

---

# 7. zip

Compress

```bash
zip project.zip project/*
```

Extract

```bash
unzip project.zip
```

---

# 8. locate

Fast file search.

```bash
locate kubeconfig
```

Update database

```bash
sudo updatedb
```

Difference:

* locate → Searches database
* find → Searches filesystem live

---

# 9. at

Schedule one-time job

```bash
at 5pm
```

Example

```text
echo "Backup"
Ctrl+D
```

View jobs

```bash
atq
```

Remove

```bash
atrm JOB_ID
```

---

# 10. Log Rotation

Purpose

Prevent logs from filling the disk.

Configuration

```text
/etc/logrotate.conf
```

Application configs

```text
/etc/logrotate.d/
```

Force rotation

```bash
logrotate -f /etc/logrotate.conf
```

---

# 11. Boot Process

Linux boot sequence

```text
Power On

↓

BIOS / UEFI

↓

Bootloader (GRUB)

↓

Kernel

↓

init/systemd

↓

Services

↓

Login Prompt
```

---

# 12. Important Configuration Files

Hosts

```text
/etc/hosts
```

DNS

```text
/etc/resolv.conf
```

Hostname

```text
/etc/hostname
```

Filesystem mounts

```text
/etc/fstab
```

User accounts

```text
/etc/passwd
```

Passwords (encrypted)

```text
/etc/shadow
```

Groups

```text
/etc/group
```

Environment

```text
/etc/profile
```

---

# 13. Useful Commands

Kernel version

```bash
uname -r
```

System information

```bash
uname -a
```

OS version

```bash
cat /etc/os-release
```

Current date

```bash
date
```

Calendar

```bash
cal
```

Disk UUID

```bash
blkid
```

---

# 14. Real-Time DevOps Interview Scenarios

## Scenario 1

Disk is 100% full.

Steps

```bash
df -h

du -sh *

find / -type f -size +500M

logrotate

rm old logs
```

---

## Scenario 2

Server inaccessible.

Checks

```bash
ping

ssh

ip addr

ip route
```

---

## Scenario 3

Application not starting.

Commands

```bash
systemctl status app

journalctl -u app

tail -100 app.log

ss -tulnp
```

---

## Scenario 4

Cannot SSH to server.

Check

* SSH service running
* Port 22 open
* Firewall rules
* Security Group / NSG (cloud)
* SSH key or password
* User permissions

---

## Scenario 5

High CPU.

Commands

```bash
top

ps -eo pid,comm,%cpu --sort=-%cpu | head

kill PID
```

---

## Scenario 6

High Memory.

Commands

```bash
free -h

top

ps -eo pid,comm,%mem --sort=-%mem | head
```

---

## Scenario 7

DNS not working.

Commands

```bash
cat /etc/resolv.conf

nslookup

dig

ping
```

---

## Scenario 8

Port already in use.

Commands

```bash
ss -tulnp

kill PID
```

---

## Scenario 9

Jenkins agent disconnected.

Checks

* Java process
* Network connectivity
* Disk space
* Agent logs
* SSH connectivity

---

## Scenario 10

Deployment successful but application unavailable.

Checks

1. Service running
2. Port listening
3. Logs
4. Firewall
5. DNS
6. Reverse proxy
7. Health endpoint
8. Load balancer configuration

---

# 15. Frequently Asked Interview Questions

### Q1. Difference between RPM and YUM?

* RPM installs individual package files.
* YUM resolves dependencies automatically and downloads packages from repositories.

---

### Q2. Difference between find and locate?

* `find` searches the live filesystem.
* `locate` searches a prebuilt database and is much faster.

---

### Q3. Difference between tar and gzip?

* `tar` archives multiple files.
* `gzip` compresses a single file.
* They are commonly combined as `.tar.gz`.

---

### Q4. Difference between SSH and SCP?

* SSH provides remote shell access.
* SCP securely copies files between systems.

---

### Q5. Which Linux commands do you use daily as a DevOps Engineer?

```text
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
systemctl
journalctl
curl
ss
ip
ping
kubectl
docker
ssh
scp
tar
```

---

# Linux Interview Rapid Revision

## File Operations

* ls
* cp
* mv
* rm
* mkdir
* touch

## Permissions

* chmod
* chown
* chgrp
* umask

## Process

* ps
* top
* kill
* pkill
* jobs
* nohup

## Disk

* df
* du
* lsblk
* mount

## Memory

* free
* vmstat

## Network

* ip
* ping
* ss
* nslookup
* dig
* curl
* traceroute

## Services

* systemctl
* journalctl

## Packages

* rpm
* yum
* dnf
* apt

## Archives

* tar
* gzip
* zip

## Remote Access

* ssh
* scp

---

# Final Linux Summary

You have now covered:

✅ Linux Architecture

✅ File System

✅ File & Directory Operations

✅ Users & Groups

✅ Permissions (`chmod`, `chown`, `chgrp`, `umask`)

✅ Hard Links & Soft Links

✅ Process Management

✅ CPU, Memory & Disk Monitoring

✅ Networking Commands

✅ DNS Troubleshooting

✅ Service Management

✅ Log Analysis

✅ Package Management

✅ SSH & SCP

✅ Archive & Compression

✅ Environment Variables

✅ Boot Process

✅ Important Configuration Files

✅ 10+ Production Troubleshooting Scenarios

✅ 25+ Common Linux Interview Questions

This completes the **Linux interview preparation** for a **4+ years DevOps Engineer**. The next logical topic is **Git**, where we'll cover branching strategies, merge vs rebase, cherry-pick, reset, revert, stash, conflict resolution, enterprise workflows, and real-time interview scenarios.


1. What is Verbose (-v)?

Verbose means show detailed information while executing a command.

Without verbose:

tar -cf backup.tar app/

Output:

(no output)

The archive is created, but you don't know what happened.

With verbose:

tar -cvf backup.tar app/

Output:

app/
app/config.yaml
app/start.sh
app/logs/
app/logs/app.log

It prints every file being processed.

You'll also see -v with other commands:

cp -v app.jar /opt/apps/

Output:

'app.jar' -> '/opt/apps/app.jar'

Verbose is mainly used for:

Troubleshooting
Monitoring long-running operations
Confirming which files were processed
2. Why do we use tar?

Imagine your application looks like this:

myapp/
│
├── app.jar
├── config.yaml
├── start.sh
└── logs/

You want to send it to another server.

Instead of copying every file individually, create one archive.

tar -cvf myapp.tar myapp/

Now:

myapp.tar

contains

myapp/

app.jar

config.yaml

start.sh

logs/

Notice:

Nothing is compressed yet.

It is just one package.

Extract
tar -xvf myapp.tar

Output

myapp/
app.jar
config.yaml
start.sh
logs/

Everything comes back exactly as it was.

3. Why .tar.gz?

A tar file is usually large.

Compress it:

tar -czvf myapp.tar.gz myapp/

Here:

c = Create
z = Compress using gzip
v = Verbose
f = Output file

Suppose your folder is:

500 MB

After compression:

myapp.tar.gz

120 MB

Much easier to transfer or store.

Extract:

tar -xzvf myapp.tar.gz
4. Difference Between tar and zip
tar
Popular on Linux.
Preserves Linux permissions and ownership.
Common for backups.

Example:

project.tar.gz
zip

Often used when sharing files with Windows users.

zip -r project.zip project/

Extract:

unzip project.zip
5. What is Log Rotation?

Imagine your application writes logs continuously.

Day 1

app.log

100 MB

Day 10

app.log

3 GB

Day 50

app.log

25 GB

Eventually:

Disk becomes full.

The application may stop writing logs or even fail.

Solution

Rotate the logs.

Instead of keeping one huge file:

app.log

Linux renames it:

app.log

↓

app.log.1

Creates a new empty file:

app.log

Now the application continues writing to the new log.

Example

Before rotation

logs/

app.log (2 GB)

Run log rotation.

After

logs/

app.log       (0 KB)

app.log.1     (2 GB)

The application now writes to:

app.log

The old log is safely stored in:

app.log.1
Does Logrotate Really Rotate?

Yes.

It actually:

Renames the current log.
Creates a new empty log.
Optionally compresses the old log.
Deletes very old logs based on your policy.
Example Configuration
/var/log/myapp/*.log {

daily

rotate 7

compress

missingok

notifempty

create 0644 appuser appgroup
}

Meaning:

daily

Rotate every day.

rotate 7

Keep only 7 old log files.

compress

Compress rotated logs.

Example:

app.log.1.gz

instead of

app.log.1
missingok

Don't fail if the log file doesn't exist.

notifempty

Don't rotate if the log is empty.

create

After rotation, create a new empty log with the specified permissions and owner.

How Logs Look Over Time

Day 1

app.log

Day 2

app.log
app.log.1.gz

Day 3

app.log
app.log.1.gz
app.log.2.gz

...

Day 8

app.log
app.log.1.gz
...
app.log.7.gz

When Day 9 rotation occurs:

app.log.7.gz

is deleted (because rotate 7), the others shift up, and yesterday's log becomes app.log.1.gz.

How Is This Used in Production?

Suppose your Spring Boot application writes to:

/opt/myapp/logs/app.log

Every day at midnight, logrotate runs (typically via cron or a systemd timer).

Before:

app.log (1.5 GB)

After rotation:

app.log        (0 KB)

app.log.1.gz   (1.5 GB)

The Java application continues writing to the new app.log.

Is Log Rotation a Backup?

No.

Log rotation is not a backup strategy.

It is a log management strategy.

For example:

Application
      │
      ▼
app.log
      │
      ▼
Logrotate
      │
      ├── app.log      (new active log)
      └── app.log.1.gz (old compressed log)

If the server's disk fails, both files are lost.

How Backup Works

A backup copies important files to another location.

Example daily backup script:

tar -czf logs_$(date +%F).tar.gz /opt/myapp/logs

This creates:

logs_2026-07-23.tar.gz

Then copy it to a backup server:

scp logs_2026-07-23.tar.gz backupuser@backup-server:/backup/logs/

Now you have:

Server: Current logs managed by logrotate
Backup Server: Archived log backup

If the application server crashes completely, you can restore the logs from the backup server.

Real Enterprise Flow
Application
      │
      ▼
app.log
      │
      ▼
Logrotate (Daily)
      │
      ├── app.log (active)
      ├── app.log.1.gz
      ├── app.log.2.gz
      └── app.log.3.gz
      │
      ▼
Nightly Backup Job
      │
      ▼
tar.gz archive
      │
      ▼
Backup Server / Cloud Storage
Interview Answer

If asked, "Is logrotate a backup tool?", you can answer:

No. Logrotate manages log files by rotating, compressing, and deleting old logs to prevent disk exhaustion. It does not create off-server backups. Backups require copying the logs or archives to another storage location such as a backup server or cloud storage.
