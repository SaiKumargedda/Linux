# Linux README – Part 3

## (Disk Management, Memory, CPU, Networking, Services & Log Troubleshooting)

---

# 1. Disk Usage - df

Shows filesystem disk usage.

```bash
df -h
```

Example Output

```text
Filesystem      Size Used Avail Use% Mounted on
/dev/sda1       100G 60G 40G 60% /
```

Options

```bash
df -h        # Human readable
df -T        # Show filesystem type
df -i        # Show inode usage
```

**Interview Tip:** If `Use%` is 100%, applications may fail to write logs or temporary files.

---

# 2. Directory Usage - du

Shows disk usage of directories/files.

```bash
du -sh /var/log
```

Output

```text
1.8G /var/log
```

Largest directories

```bash
du -sh * | sort -hr
```

Largest files

```bash
find / -type f -size +500M
```

---

# 3. lsblk

Displays block devices.

```bash
lsblk
```

Output

```text
NAME    SIZE TYPE MOUNTPOINT
sda     100G disk
├─sda1   99G part /
└─sda2    1G part /boot
```

---

# 4. fdisk

View partitions

```bash
sudo fdisk -l
```

Commonly used when adding new disks.

---

# 5. Mount Filesystem

Mount

```bash
sudo mount /dev/sdb1 /data
```

Unmount

```bash
sudo umount /data
```

View mounted filesystems

```bash
mount
```

or

```bash
findmnt
```

---

# 6. free

Check memory usage.

```bash
free -m
```

Output

```text
              total used free shared buff/cache available
Mem:           4096 2300 500 120 1296 1450
```

Human readable

```bash
free -h
```

---

# 7. /proc/meminfo

Detailed memory statistics.

```bash
cat /proc/meminfo
```

Important fields

* MemTotal
* MemFree
* Buffers
* Cached
* SwapTotal
* SwapFree

---

# 8. vmstat

Virtual memory statistics.

```bash
vmstat 2 5
```

Shows

* CPU
* Memory
* Swap
* I/O
* Context switches

Useful for performance troubleshooting.

---

# 9. lscpu

CPU information.

```bash
lscpu
```

Shows

* CPU architecture
* Number of CPUs
* Cores
* Threads
* Virtualization support

---

# 10. top

Real-time monitoring.

```bash
top
```

Monitor

* CPU
* Memory
* Processes
* Load Average

---

# 11. sar

Historical performance statistics.

```bash
sar -u
```

Memory

```bash
sar -r
```

Disk

```bash
sar -d
```

Network

```bash
sar -n DEV
```

---

# 12. ip

View IP address.

```bash
ip addr
```

Routing table

```bash
ip route
```

---

# 13. ping

Connectivity check.

```bash
ping google.com
```

Limited packets

```bash
ping -c 4 google.com
```

---

# 14. traceroute

Shows packet path.

```bash
traceroute google.com
```

Useful for network latency troubleshooting.

---

# 15. nslookup

DNS lookup.

```bash
nslookup google.com
```

Output

```text
Address: 142.250.xxx.xxx
```

---

# 16. dig

Detailed DNS lookup.

```bash
dig google.com
```

Specific record

```bash
dig google.com A
```

---

# 17. curl

Check API or website.

```bash
curl https://example.com
```

Headers only

```bash
curl -I https://example.com
```

Verbose

```bash
curl -v https://example.com
```

Download file

```bash
curl -O https://example.com/file.zip
```

---

# 18. wget

Download files.

```bash
wget https://example.com/file.zip
```

Resume download

```bash
wget -c https://example.com/file.zip
```

---

# 19. ss

View listening ports and connections.

```bash
ss -tuln
```

Output

```text
LISTEN
0 128 *:22
0 128 *:443
```

---

# 20. netstat

Older networking utility.

```bash
netstat -tulnp
```

Useful on older Linux systems.

---

# 21. hostname

Display hostname.

```bash
hostname
```

---

# 22. hostnamectl

Detailed host information.

```bash
hostnamectl
```

---

# 23. systemctl

Check service status

```bash
systemctl status nginx
```

Start

```bash
systemctl start nginx
```

Stop

```bash
systemctl stop nginx
```

Restart

```bash
systemctl restart nginx
```

Enable at boot

```bash
systemctl enable nginx
```

Disable

```bash
systemctl disable nginx
```

---

# 24. journalctl

View system logs.

Latest logs

```bash
journalctl
```

Specific service

```bash
journalctl -u nginx
```

Follow logs

```bash
journalctl -f
```

Today's logs

```bash
journalctl --since today
```

---

# 25. tail

View latest logs.

```bash
tail -100 app.log
```

Live logs

```bash
tail -f app.log
```

---

# 26. grep in Logs

Search errors

```bash
grep ERROR app.log
```

Ignore case

```bash
grep -i error app.log
```

Count matches

```bash
grep -c ERROR app.log
```

---

# 27. Real-Time Troubleshooting Scenarios

## Scenario 1

Disk Full

Commands

```bash
df -h
du -sh *
find / -type f -size +500M
```

Actions

* Remove unnecessary files
* Clean old logs
* Rotate logs
* Extend disk if required

---

## Scenario 2

High Memory Usage

Commands

```bash
free -h
top
ps -eo pid,comm,%mem --sort=-%mem | head
```

Actions

* Identify memory-intensive process
* Restart application if needed
* Tune JVM/application
* Increase memory if justified

---

## Scenario 3

High CPU Usage

Commands

```bash
top
ps -eo pid,comm,%cpu --sort=-%cpu | head
```

Actions

* Identify high CPU process
* Check application logs
* Optimize workload or restart service

---

## Scenario 4

Application Not Accessible

Checks

```bash
systemctl status app
ss -tuln
curl http://localhost:8080/health
ping <server>
nslookup <hostname>
```

---

## Scenario 5

Service Not Starting

Commands

```bash
systemctl status app
journalctl -u app
tail -100 /var/log/app.log
```

---

## Scenario 6

DNS Issue

Commands

```bash
nslookup app.example.com
dig app.example.com
cat /etc/resolv.conf
```

---

## Scenario 7

Port Already in Use

Commands

```bash
ss -tulnp
```

or

```bash
netstat -tulnp
```

Identify the process and stop or reconfigure it if appropriate.

---

# Frequently Asked Interview Questions

### Q1. Difference between df and du?

* **df**: Shows filesystem-level disk usage.
* **du**: Shows directory/file-level disk usage.

---

### Q2. Difference between curl and wget?

* **curl**: Used for APIs, testing endpoints, custom HTTP requests.
* **wget**: Primarily used for downloading files.

---

### Q3. Difference between netstat and ss?

* **ss** is newer, faster, and preferred.
* **netstat** is older but still found on some systems.

---

### Q4. How do you troubleshoot if an application is not accessible?

1. Check process/service status.
2. Check listening ports.
3. Verify firewall/security rules if applicable.
4. Test locally with `curl`.
5. Review application and system logs.
6. Verify DNS if using a hostname.
7. Check network connectivity.

---

### Q5. Which Linux commands do you use daily?

```text
df
du
free
top
ps
systemctl
journalctl
tail
grep
ss
curl
ip
ping
hostname
lsblk
```

---

# Linux Part 3 Summary

✅ Disk Management (`df`, `du`, `lsblk`, `fdisk`, `mount`)

✅ Memory Monitoring (`free`, `/proc/meminfo`, `vmstat`)

✅ CPU Monitoring (`lscpu`, `top`, `sar`)

✅ Networking (`ip`, `ping`, `traceroute`, `nslookup`, `dig`, `curl`, `wget`, `ss`, `netstat`)

✅ Service Management (`systemctl`)

✅ Log Analysis (`journalctl`, `tail`, `grep`)

✅ Real-Time Production Troubleshooting

✅ DevOps Interview Scenarios

That's a great question. The answer depends on whether you're talking about a hard link or a soft link.

Hard Link

Initially, both filenames point to the exact same data on disk.

Example:

echo "Hello DevOps" > report.txt

ln report.txt backup.txt

Now:

cat report.txt

Output:

Hello DevOps
cat backup.txt

Output:

Hello DevOps

If you modify one file:

echo "New Content" > report.txt

Now check both:

cat report.txt
New Content
cat backup.txt
New Content

Why?

Because there aren't actually two separate files with two separate copies of the data. There are two filenames (directory entries) pointing to the same inode, and that inode points to the same data blocks.

report.txt ----\
                \
                 --> Inode 13521 --> Data: "New Content"
                /
backup.txt ----/

So changing the content through either filename changes the same underlying data.

Soft Link

A soft link is different. It's just a pointer (shortcut) to another file.

ln -s report.txt shortcut.txt

If report.txt changes, shortcut.txt also shows the updated content because it accesses report.txt.

However, if you delete report.txt:

rm report.txt

Then:

cat shortcut.txt

Output:

cat: shortcut.txt: No such file or directory

The soft link is now broken because its target no longer exists.
