# RHCSA Exam Complete Guide

## **Primary Machine**

### **Q2: Yum Repository Configuration**
#### **Steps:**
```sh
vim /etc/yum.repos.d/exam.repo
```
_Add the following content:_
```
[App]
Name=AppStream
Baseurl= https://repo.almalinux.org/almalinux/9/AppStream/x86_64/os
Enabled=1
Gpgcheck=0

[Base]
Name=BaseOS
Baseurl=https://repo.almalinux.org/almalinux/9/BaseOS/x86_64/os
Enabled=1
Gpgcheck=0
```
```sh
yum repolist
yum install -y vsftpd
```

### **Q3: Debug SE-Linux**
#### **Steps:**
```sh
semanage port -a -t http_port_t -p tcp 82
firewall-cmd --add-port=82/tcp --permanent
firewall-cmd --reload
systemctl restart httpd
systemctl enable httpd
```

### **Q4: Configure a Cron Job for User Neha**
#### **Steps:**
```sh
crontab -eu neha
```
_Add the following lines:_
```
23 14 * * * /bin/echo hiya
*/3  *  * * * /bin/echo hiya
```

### **Q5: User, Group, and Membership Configuration**
#### **Steps:**
```sh
groupadd sysadmin
useradd -G sysadmin natasha
useradd -G sysadmin sarah
useradd -s /sbin/nologin harry
passwd natasha
passwd sarah
passwd harry
```

### **Q6: Create Collaborative Directory**
#### **Steps:**
```sh
mkdir -p /common/admin
chgrp sysadmin /common/admin/
chmod g+w, o=--- /common/admin/
chmod g+s /common/admin/
```

### **Q7: Configure NTP Client**
#### **Steps:**
```sh
vim /etc/chrony.conf
```
_Add the following line:_
```
server 2.in.pool.ntp.org iburst
```
```sh
systemctl restart chronyd.service
systemctl enable chronyd.service
timedatectl
```

### **Q8: Find and Copy Files Owned by User Simone**
#### **Steps:**
```sh
useradd simone
passwd simone
visudo
```
_Add the following line:_
```
simone ALL=(ALL) ALL
```
```sh
su simone
mkdir found
find / -user simone -exec cp -arvf {} /root/found \;
```

### **Q9: Find and Save Specific String in a File**
#### **Steps:**
```sh
grep strato /usr/share/dict/words > /searchfile
cat /searchfile
```

### **Q11: Set Default Permissions for User Alex**
#### **Steps:**
```sh
su - alex
vim .bashrc
```
_Add the following line:_
```
umask 222
```

### **Q12: Create a Script to List Files Below 10MiB in /usr**
#### **Steps:**
```sh
vim /usr/local/bin/mysearch
```
_Add the following lines:_
```sh
find /usr -size -10M > /root/lines
```
```sh
chmod a+x /usr/local/bin/mysearch
mysearch
```

### **Q13: Create a User with Specific UID**
#### **Steps:**
```sh
useradd -u 2112 barry
passwd barry
```

### **Q14: Sudo Privileges for Group 'elite'**
#### **Steps:**
```sh
groupadd elite
visudo
```
_Add the following line:_
```
%elite ALL=(ALL) NOPASSWD: ALL
```

---

## **Secondary Machine**

### **Q1: Crack Root Password**
#### **Steps:**
1. Restart and press `ESC`.
2. Press `e` and add `rd.break` in the second-last line.
3. Run the following commands:
```sh
mount -o remount,rw /sysroot/
chroot /sysroot/
passwd
```
4. Then execute:
```sh
touch /.autorelabel
exit
exit
```

### **Q2: Set a Recommended Tuning Profile**
#### **Steps:**
```sh
yum install -y tuned
systemctl start tuned
systemctl enable tuned
tuned-adm recommend
tuned-adm profile virtual-guest
```

### **Q3: Create a Backup of /etc Directory**
#### **Steps:**
```sh
yum install -y bzip2
tar -cvjf /home/backup.tar.bz2 /etc
tar -cvzf /home/backup.tar.gz /etc
```

### **Q4: Password Policy - Change Password Every 20 Days**
#### **Steps:**
```sh
vim /etc/login.defs
```
_Add the following line:_
```
PASS_MAX_DAYS = 20
```

### **Q5: Create and Build a Container from a Given Containerfile**
#### **Steps:**
```sh
ssh andrew@localhost
wget https://raw.githubusercontent.com/sunilkumar0633/Git_Test/master/Containerfile
podman image build -t watcher .
podman image ls
```

### **Q6: Create and Run a Container as a Systemd Service**
#### **Steps:**
```sh
mkdir /opt/files
mkdir /opt/processes
chown andrew:andrew /opt/files
chown andrew:andrew /opt/processes
ssh andrew@localhost
podman container run -d --name ascii2pdf -v /opt/files:/opt/incoming:Z -v /opt/processes:/opt/outgoing:Z watcher
podman ps
mkdir -p ~/.config/systemd/user/
cd ~/.config/systemd/user/
podman generate systemd --name ascii2pdf --new --files
systemctl --user daemon-reload
systemctl --user start container-ascii2pdf.service
systemctl --user enable container-ascii2pdf.service
loginctl enable-linger
```

### **Q7: Create a Container from Red Hat Registry**
#### **Steps:**
```sh
ssh andrew@localhost
podman login registry.redhat.io
podman image pull watcher
podman image ls
```
```sh
mkdir /opt/files
mkdir /opt/processes
chown andrew:andrew /opt/files
chown andrew:andrew /opt/processes
ssh andrew@localhost
podman container run -d --name ascii2pdf -v /opt/files:/opt/incoming:Z -v /opt/processes:/opt/outgoing:Z watcher
podman ps
mkdir -p ~/.config/systemd/user/
cd ~/.config/systemd/user/
podman generate systemd --name ascii2pdf --new --files
systemctl --user daemon-reload
systemctl --user start container-ascii2pdf.service
systemctl --user enable container-ascii2pdf.service
loginctl enable-linger
```

