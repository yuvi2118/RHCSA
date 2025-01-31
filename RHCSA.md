On Primary Machine:

Ques no:2  
Yum repository configuration on machines  
baseurl \= https://repo.almalinux.org/almalinux/9/AppStream/x86\_64/os  
baseurl \= [https://repo.almalinux.org/almalinux/9/BaseOS/x86\_64/os](https://repo.almalinux.org/almalinux/9/BaseOS/x86_64/os)

Ans :- vim /etc/yum.repos.d/exam.repo

\[App\]  
Name=AppStream  
Baseurl= https://repo.almalinux.org/almalinux/9/AppStream/x86\_64/os  
Enabled \=1  
Gpgcheck \=0

\[Base\]  
Name=  
Baseurl=[https://repo.almalinux.org/almalinux/9/BaseOS/x86\_64/os](https://repo.almalinux.org/almalinux/9/BaseOS/x86_64/os)  
Enabled \=1  
Gpgcheck \=0

yum repolist  
yum install \-y vsftpd

Ques no:3  
Debug SE-Linux  
http service serve non-standard 82 port for your machine, the system  
is not able to connect to httpd service at port 82, fix the debug issue,  
to store the HTML files under /var/www/html directory don’t have  
change to it. it should be accessible at port 82 and should start at boot  
time.

Ans:- 

semanage port \-a \-t http\_port\_t \-p tcp 82

firewall-cmd \--add-port=82/tcp \--permanent

firewall-cmd  \--reload

systemctl restart httpd

systemctl enable httpd

Ques no:4  
Configure a cron job on Primary machine •The user Neha must configure a cron job that runs daily at 14:23 local  
time and executes /bin/echo hiya OR • The user Neha must configure  
a cron job that runs daily at every 3 minute local time and executes  
/bin/echo hiya

Ans:-   
crontab \-eu neha

(in vim editor)  
23 14 \* \* \* /bin/echo hiya  
\*/3  \*  \* \* \* /bin/echo hiya

(e.g min   hour    date   month    day)

Q5.) Create the following users, groups, and group  
memberships: \-  
A group named sysadmin. A user natasha who belongs to sysadmin  
as a secondary group. A user sarah who also belongs to sysadmin as  
a secondary group. A user harry who does not have access to an  
interactive shell on the system, and who is not a member of sysadmin.  
Natasha, Sarah and Harry should all have the password of thuctive

Ans:- 

groupadd sysadmin

useradd \-G sysadmin natasha

useradd \-G sysadmin sarah

useradd \-s /sbin/nologin/ harry

passwd natasha  
passwd sarah

passwd harry

Q6). Create a collaborative directory “/common/admin” with the  
following characteristics:  
Group ownership of /common/admin is sysadmin. The directory  
should be readable, writable, and accessible to members of sysadmin,  
but not to any other user. (It is understood that root has access to all  
files and directories on the system.) Files created in /common/admin  
automatically have group ownership set to the sysadmin group.

Ans:- 

mkdir \-p  /common/admin

chgrp sysadmin /common/admin/

ls \-l /common/

chmod g+w, o=--- /common/admin/

chmod g+s /common/admin/

ls \-l /common/

Q7). Configure NTP in your system so that it is an NTP client of  
*2.in.pool.ntp.org*

Ans:-

vim /etc/chrony.conf

(In vim editor)

Add:- server.2.in.pool.ntp.org iburst

systemctl restart chronyd.service

systemctl enable chronyd.service

timedatectl

*Q8). Find the files in your system which is owned by Simone user*  
*& copy all the files on /root/found directory*

Ans:-

Run At Root

useradd simone  
passwd simone  
visudo

Add At Allow to run command Anywhere

simone ALL=(ALL)		ALL

su simone

mkdir found

find / \-user simone \-exec cp \-arvf {} /root/found \\;

Q9). Find the string strato from /usr/share/dict/words and save  
the result in /searchfile.

Ans:- At Root

grep stratro /usr/share/dict/words \>/searchfile

cat searchfile

Will List All words with strato

Q11.) • set default permissions for user alex for all newly created files  
and folders • set permissions to the all newly created files r--r--r– • set  
permissions to the all newly created directory r-xr-xr-x

Ans:-   
su \- alex

vim .bashrc

(under unset rc)  
umask 222

Q-12) • Write a script mysearch to list the contents of /usr that are  
below 10Mib. • The script should be present in /usr/local/bin • Afterexecution, the script should automatically write all the lines and save It  
to /root/lines

Ans:-

vim /usr/local/bin/mysearch

(In Vim Editor) 

find /usr \-size  \-10M \>/root/lines  
find /usr \-size \+20k \-size \-50k \>/root/lines  
find /usr \-size \-10M \-perm /g=s \>/root/lines (using a )

chmod a+x /usr/local/bin/mysearch  
mysearch

Q13). User of Specific UID Create a user barry User id of this user  
should be 2112 and set password Atenorth

Ans:- 

useradd \-u 2112  barry

passwd barry

Password \=  Atenorth

Id \-u barry

14\. Sudo privilege a group name is 'elite', they have to give  
administrative permission without password.

Ans:-

groupadd elite

visudo  
Without Password   
%elite 	ALL=(ALL) 		NOPASSWD: ALL

On Secondary Machine:

Q1.) First step is to crack password of Secondary Machine. New  
password is redhat@00

Ans:- 

Restart press “ESC”  
Then press “e”  
Add in second last line  
Rd.break

Commands

mount \-o remount,rw /sysroot/  
chroot /sysroot/  
passwd 

touch /.autorelabel  
exit  
exit

Q2.) Set a recommended tuning profile for your system. (Profile  
already available)

Ans-\> Install tuned package if not installed.

yum install \-y tuned

systemctl start tuned

systemctl enable tuned

tuned-adm recommend  
   
tuned-adm profile virtual-guest

Q3). Create a backup.tar.(bz2 or gz) of /etc directory in /home location. NOTE-\> If sometimes bz2 not work because bzip2 not installed so first install the package 

Ans:-

yum install-y bzip2

tar \-cvjf /home/backup.tar.bz2 /etc

tar \-cvzf /home/backup.tar.gz /etc

Q4). Password policy , change password after 20 days

Ans:-

vim /etc/login.defs  
	PASS\_MAX\_DAYS \= 20

 Q5). Create a container on node1 as Andrew  using [https://raw.githubusercontent.com/sunilkumar0633/Git\_Test/master/Containerfile](https://raw.githubusercontent.com/sunilkumar0633/Git_Test/master/Containerfile)  
build the image name is watcher, don't change the Containerfile content-

 Ans:-

        ssh andrew@localhost

        Wget [https://raw.githubusercontent.com/sunilkumar0633/Git\_Test/master/Containerfile](https://raw.githubusercontent.com/sunilkumar0633/Git_Test/master/Containerfile)

        podman image build \-t watcher .

        Podman image ls

Q6).  create a container using an image which u created somewhere in exam:-

•         create a container using Andrew user and container name should be ascii2pdf

•         container should run as a systemd service, so configure as a service name container-ascii2pdf.service

•         container should run at boot time

•         container name should be ascii2pdf

•         mount /opt/files directory to /opt/incoming in container and /opt/processes to /opt/outgoing in container

   	this container will convert ascii test file into pdf format, so when you create simple file in /opt/files then container will automatically convert that file into pdf and save /opt/processed

 

Ans:-

        mkdir /opt/files

       mkdir /opt/processes

       chown andrew:andrew /opt/files

        chown andrew:andrew /opt/processes

      ssh andrew@localhost \[use this command to login, not su\]

      podman container run \-d \--name ascii2pdf \-v /opt/files:/opt/incoming:Z \-v /opt/processes:/opt/outgoing:Z watcher

         podman ps

         mkdir \-p  \~/.config/systemd/user/

         cd  \~/.config/systemd/user/

         podman generate systemd  \--name ascii2pdf  \--new  \--files

         systemctl   \--user   daemon-reload

         systemctl   \--user   start   container-ascii2pdf.service

         systemctl   \--user   enable  container-ascii2pdf.service

         loginctl   enable-linger

Q7).  Create a container on node1 as andrew  :-

Create a container using the image watcher. Images is stored on registry.redhat.io

create a container using andrew user

           	container should run as a systemd service, so configure as a service name container-

           	ascii2pdf.service

           	mount /opt/files directory to /opt/incoming in container and /opt/processes to

          	/opt/outgoing in container

   	this container will convert ascii test file into pdf format, so when you create simple file in /opt/files then container will automatically convert that file into pdf and save /opt/processed

 registry url \- registry.redhat.io

         	Login user \- in89933217

        	Password \- Shivani@198

NOTE:- login creds will given on imp configuration information section where your node1 root password mentioned

 	Ans:-

         ssh andrew@localhost

         podman login registry.redhat.io

         podman image pull codesxchange/watcher ( this command for only practice don’t use it in exam & select \- docker.io/codesxchange/watcher:latest )

         podman image pull watcher ( In exam use this command to pull image )

         podman image ls

	User root user from here

         mkdir /opt/files

         mkdir /opt/processes

         chown andrew:andrew /opt/files

         chown andrew:andrew /opt/processes

         ssh andrew@localhost \[use this command to login, not su\]

         podman container run \-d \--name ascii2pdf \-v /opt/files:/opt/incoming:Z \-v /opt/processes:/opt/outgoing:Z watcher­­

         podman ps

         mkdir \-p  .config/systemd/user/

         cd  \~/.config/systemd/user/

         podman generate systemd  \--name ascii2pdf  \--new  \--files

         systemctl   \--user   daemon-reload

         systemctl   \--user   start   container-ascii2pdf.service

         systemctl   \--user   enable  container-ascii2pdf.service

         loginctl   enable-linger

