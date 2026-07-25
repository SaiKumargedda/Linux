1️⃣ File & Directory Management

These commands are used daily to navigate filesystem, manage logs, configs, and artifacts.

ls -lrt

Purpose: List files with details sorted by latest modified time.

ls -lrt

Options:

l → long format

r → reverse

t → sort by time

DevOps Use:

Checking recent logs or changed deployment files.

cd

Change directory.

cd /var/log

Used for navigation between application directories.

pwd

Print current directory.

pwd

Important before running delete commands in production.

cp

Copy files or directories.

cp app.yaml app.yaml.bak
cp -r config/ backup/

DevOps Use:

Backup configs before modification.

mv

Move or rename files.

mv old.log new.log
mv app.jar /opt/app/

Used during deployments and log rotation.

rm -rf

Delete files/directories forcefully.

rm -rf temp/

⚠️ Dangerous — use carefully.

mkdir

Create directory.

mkdir logs
mkdir -p /opt/app/config

-p creates parent directories.

find

Search files.

find /var/log -name "*.log"
find / -type f -size +1G

Used to locate logs or large files.

stat

Shows detailed file metadata.

stat app.log

Used for permission and timestamp verification.

du -sh

Shows directory size.

du -sh /var/*

Used for disk troubleshooting.

df -h

Shows filesystem usage.

df -h

Used to check disk space alerts.

2️⃣ File Viewing & Text Processing (Log Analysis)

Very important for troubleshooting.

cat

Display file content.

cat config.yaml

Use for small files only.

less

View large files page by page.

less app.log

Better than cat for logs.

head

Show first lines.

head -n 20 app.log

Used to check file structure.

tail -f

Live log monitoring.

tail -f app.log

⭐ Critical DevOps command.

grep

Search text pattern.

grep ERROR app.log
grep -i fail app.log

Used to find errors quickly.

awk

Column-based text processing.

awk '{print $1}' access.log

Extracts first column.

Example:

awk '$9 == 500' access.log

Used for log analysis.

sed

Stream editor (replace text).

sed 's/ERROR/WARN/g' app.log
sed -i 's/dev/prod/g' config.yaml

Used for automated config updates.

cut

Extract columns using delimiter.

cut -d':' -f1 /etc/passwd

Used for structured files.

sort

Sort lines.

sort file.txt
uniq

Remove duplicates.

sort file.txt | uniq
sort file.txt | uniq -c
wc -l

Count lines.

wc -l app.log
grep ERROR app.log | wc -l

Used for metrics and validation.

3️⃣ Process & System Monitoring

Used for performance troubleshooting.

ps -ef

List running processes.

ps -ef | grep java

Check application status.

top

Real-time CPU and memory usage.

top

First command for slow system.

htop

Interactive version of top.

htop
free -m

Memory usage.

free -m

Used during OOM issues.

uptime

System running time and load.

uptime
vmstat

Performance statistics.

vmstat 2

Used for deeper performance analysis.

iostat

Disk I/O stats.

iostat -x 2

Used for storage bottlenecks.

lsof

Open files and ports.

lsof -i :8080

Used for port conflicts.

watch

Run command repeatedly.

watch df -h

Continuous monitoring.

4️⃣ Disk & Storage Management

Used for disk issues and mounting.

lsblk

List disks and partitions.

lsblk

Used after adding cloud disk.

mount

Attach filesystem.

mount /dev/sdb1 /data

Used for NFS or volumes.

umount

Detach filesystem.

umount /data

Before disk removal.

5️⃣ Networking & Connectivity

Critical for microservices debugging.

ping

Check connectivity.

ping google.com
curl

HTTP request testing.

curl http://localhost:8080/health
curl -I http://example.com

⭐ Most important networking command.

wget

Download files.

wget https://example.com/file
ss -tulnp

Check listening ports.

ss -tulnp

Modern replacement for netstat.

netstat -tulnp

Older port tool.

netstat -tulnp
traceroute

Network path analysis.

traceroute google.com
nslookup

DNS lookup.

nslookup service
dig

Advanced DNS lookup.

dig google.com
telnet

Port connectivity test.

telnet localhost 3306
nc (netcat)

Modern port testing.

nc -zv host 443
6️⃣ Permissions & Ownership

Used for access issues.

chmod

Change permissions.

chmod 755 script.sh
chmod +x deploy.sh
chown

Change owner.

chown appuser:appgroup /opt/app
chgrp

Change group.

chgrp docker /var/run/docker.sock
id

User identity.

id appuser
whoami

Current user.

whoami
7️⃣ Package Management

Install and manage software.

yum

RHEL package manager.

yum install docker -y
dnf

Modern yum.

dnf install java-17 -y
apt

Ubuntu package manager.

apt update
apt install nginx -y
rpm

List packages (RHEL).

rpm -qa | grep docker
dpkg

List packages (Ubuntu).

dpkg -l | grep nginx
8️⃣ User & Session Management

Used for access control.

who

Logged-in users.

who
w

User activity.

w
last

Login history.

last
su

Switch user.

su - appuser
sudo

Admin privileges.

sudo su -
passwd

Change password.

passwd appuser
9️⃣ Archive & Compression

Used for backups and transfer.

tar

Archive and compress.

tar -czf logs.tar.gz /var/log
tar -xzf logs.tar.gz
zip

Create zip archive.

zip reports.zip file1 file2
unzip

Extract zip.

unzip reports.zip
gzip

Compress file.

gzip large.log
gunzip

Decompress file.

gunzip large.log.gz
🔟 Automation & Environment

Used in CI/CD and scripting.

bash

Run script.

bash deploy.sh
sh

Run shell script.

sh cleanup.sh
crontab

Schedule tasks.

crontab -e
crontab -l

Example:

0 2 * * * /home/user/backup.sh
env

Show environment variables.

env
export

Set environment variable.

export JAVA_HOME=/usr/lib/jvm/java-17
⭐ Real DevOps Troubleshooting Flow Examples
Disk full
df -h
du -sh /*
Service not reachable
ping host
nslookup host
nc -zv host 8080
curl http://host:8080
Application slow
top
ps -ef
free -m
