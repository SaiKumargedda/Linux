1. What is Linux?

Linux is an open-source Unix-like operating system kernel developed by Linus Torvalds.

An operating system manages:

CPU
Memory
Disk
Network
Processes
Hardware resources

In DevOps, Linux is the most widely used OS for servers, containers, Kubernetes nodes, and CI/CD agents.

2. Linux Architecture
+----------------------+
|      Applications    |
+----------------------+
|         Shell        |
+----------------------+
|        Kernel        |
+----------------------+
|      Hardware        |
+----------------------+
Hardware

Physical components:

CPU
RAM
Disk
Network Card
Kernel

Core of Linux. Responsible for:

Process Management
Memory Management
File System
Device Drivers
Networking
Security
Shell

Accepts user commands and passes them to the kernel.

Examples:

bash
sh
zsh
Applications

Programs like:

Docker
Jenkins
Git
kubectl
Terraform
3. Linux Distributions

Popular distributions:

Ubuntu
RHEL (Red Hat Enterprise Linux)
CentOS
Rocky Linux
AlmaLinux
Debian
SUSE

Interview Answer:

In my projects, I primarily worked on RHEL-based Linux servers for Jenkins agents and Kubernetes worker nodes.

4. Important Linux Directories
Directory	Purpose
/	Root directory
/home	User home directories
/root	Root user's home
/etc	Configuration files
/var	Logs, mail, spool files
/tmp	Temporary files
/opt	Optional software
/usr	User programs and binaries
/bin	Essential user commands
/sbin	System administration commands
/lib	Shared libraries
/dev	Device files
/proc	Process and kernel information
/sys	Kernel and hardware information
/mnt	Temporary mount points
/media	Removable media
5. Navigating the File System
Current directory
pwd

Output

/home/devops
List files
ls

Long listing

ls -l

Example Output

-rw-r--r-- 1 devops devops 450 Jul 23 file.txt

Explanation:

-rw-r--r--

|  |  |  |

|  |  |  +-- Others

|  |  +----- Group

|  +-------- Owner

+----------- File Type

Hidden files

ls -la

Sort by time

ls -ltr
6. Changing Directory

Go to home

cd

Go to root

cd /

Go one level up

cd ..

Previous directory

cd -
7. Creating Files & Directories

Create directory

mkdir project

Nested directories

mkdir -p dev/app/config

Create file

touch file.txt

Multiple files

touch file1 file2 file3
8. Copy Commands

Copy file

cp file1.txt file2.txt

Copy directory

cp -r app backup
9. Move/Rename

Rename

mv old.txt new.txt

Move

mv file.txt /tmp/
10. Delete

Delete file

rm file.txt

Delete directory

rm -r project

Force delete

rm -rf project

⚠️ Interview Note: Always use rm -rf carefully. Accidentally deleting critical directories can cause major outages.

11. Display File Content

Display file

cat file.txt

Beginning of file

head file.txt

First 20 lines

head -20 file.txt

Last 10 lines

tail file.txt

Follow logs continuously

tail -f application.log

Real-time Example:

tail -f /var/log/messages

or

tail -f catalina.out
12. Count Lines, Words & Characters
wc file.txt

Output

20 150 1200 file.txt

Meaning:

20 lines
150 words
1200 characters

Only line count

wc -l file.txt
13. File Information
file script.sh

Output

Bourne-Again shell script
14. Absolute vs Relative Path

Absolute

/home/devops/scripts/deploy.sh

Relative

scripts/deploy.sh
15. Locate Commands

Find executable

which kubectl

Output

/usr/bin/kubectl

Find command details

whereis docker

Output

docker: /usr/bin/docker
16. Command History
history

Repeat last command

!!

Execute command number

!105

Search history

history | grep kubectl
17. Clear Screen
clear

Shortcut

Ctrl + L
Real-Time Interview Questions
Q1. Which Linux distributions have you worked on?

Answer:

Primarily RHEL-based Linux systems. I also have familiarity with Ubuntu, especially in containerized environments and lab setups.

Q2. Which directories do you use most frequently?

Answer:

/etc – Configuration files
/var/log – Application and system logs
/tmp – Temporary files
/home – User files
/opt – Application installations
/proc – Process troubleshooting
Q3. Where are logs stored in Linux?

Answer:

Most system logs are under /var/log. Application logs depend on the application (for example, Tomcat uses catalina.out by default).

Q4. Difference between Absolute and Relative Path?

Answer:

Absolute path starts from /.
Relative path starts from the current working directory.
DevOps Commands Used Daily
pwd
ls -ltr
cd
mkdir
touch
cp
mv
rm
cat
head
tail -f
history
which
whereis
wc
file
