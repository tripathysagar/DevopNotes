- `sudo ls -l /sbin/init` : init process used by the system
- `sudo systemctl get-default` : default systemd target
- `sudo systemctl set-default multi-user.target` : change systemd target
- `sudo file <object>` : file type 
- `/opt` : forlder for installing user app
- `/dev` : block devices that are present by running lsblk cmd
- `lshw` : for hardware of the system

---
## RPM Package cmd

- install : `rpm -ivh vim.rpm` 
- uninstall : `rpm -e vim.rpm`
- upgrade : `rpm --Uvh vim.rpm`
- query : `rpm -q vim.rpm`
- verifying : `rpm -Vf <vim-file>`
### `yum` 
 - RPM based pkg 
 - software repo
 - high-level pkg manager, install dependency
 - autometic dependency reolution
 - saved under `/etc/yum.repos.d`
 - red hat sys comes with own repo: `/etc/yum.repos.d/redhat.repo`
 - user can update any third party repo
 - list all the repos `yum repolist`
 - list packge for a command `yum provides httpd`
 - remove package `yum remove httpd`
 - update packge `yum update httpd`
 - to install with without asking (y/n) `sudo yum install firefox -y`

 ---

## DPKG 
- install : `dpkg -i vim.deb` 
- uninstall : `rpm -r vim.deb`
- upgrade : `rpm -l vim.deb`
- query : `rpm -s vim.deb`
- verifying : `rpm -p <vim-file>`
### `apt` 
 - dpkg based pkg 
 - software repo
 - high-level pkg manager, install dependency
 - autometic dependency reolution
 - refresh package `apt update`
 - upgrade package `apt upgrade`
 - update repos `apt edit-sources`
 - install `apt install httpd`
 - remove `apt remove httpd`
 - search `apt search httpd`

---

## basic scripting

- `du -sk <file>` : shows the file size in KB
- `du -sh <file>` : shows file in a human readable format
- `ls -lh <file>` : list file
- `tar -cf temp.tar file1 file2 file3` : to compress a list of files`c`: archive `f`: file name to be created
- `tar -tf tmp.tar` : to see the content of the tmp.tar file
- `tar -xf tmp.tar` : to extract the tmp.tar file
- `tar -zcf temp.tar file1 file2 file3` `-z` flag for reducing the size futher of the compressed one

| command compress | encoded file | command decompress|
|----------|----|----|
|bzip2 test.img| test.img.bz2| bunzip2 test.img.bz2|
|gzip test.img| test.img.gz| gunzip test.img.gz|
|xz test.img| test.img.xz| unxz test.img.xz|

- `zcat`|`bzcat`|`xzcat` : can be used to read the compressed files without extraction
- `locate <file>` : for locating file but dependent on `mlocate.db`. finding is dependent upon the db status. update db `updatedb`
- `find <dir>/. -name <file>` find the file location in the `<dir>`. For `.` present directory
- `grep <pattern> <file>` : for searching pattern in a file
- `grep -i <pattern> <file>` : for searching pattern in a file irrespective of the case sensetivity
- `grep -r <pattern> <dir>` : for searching pattern recurssivelyin a directory
-  `grep -V <pattern> <file>` : not showing lines that contains pattern
- `grep -w <pattern> <file>` : will return only the lines matching pattern not the sub-string matching
- `grep -A20 -B10 <pattern> <file> `: will print 20 lines after the pattern and 10 lines before the pattern
- `echo "hello" > temp.txt`: will create file temp.txt if it dont exist and put the "hello" inside of it
- `echo "hello" >> temp.txt`: will append file temp.txt with "hello" inside of it
- `cat file_not_exist 2> error.txt` : will send std error to the file
- `|` can be used to chain the commands. First cmd std output will be std input to the second cmd


---

## Linux account

Each account has username, UID, GID, Home directory and Default shell
- `id username` : retruns all those details
- superuser account : UID = 0
- system account (ssh, mail) UID <100 or 500-1000
- service account( nginx)
- `who` current user details
- `last` last logged in user to the system
- `grep -i ^uname /etc/passwd` returns `Username:Passwd:UID:GID:GECOS:Home-dir:shell`
- `sudo grep <username> /etc/sudoers` : for checking permission of a user
- `/etc/group` : for showing the gorups
- `sudo useradd -u 1010 -g 1010 -s /bin/sh john` : creates a user john with uid : 101 group :1010 and shell : /bin/sh
- `sudo passwd john` : to set passwordfo an user

- `chmod u+rwx <file>` : give full access to the owner
- `chmod ugo+r-x <file>` : give read access to owners, groups and others.  Remove execute access
- `chmod o-rwx <file>` : remove all access
- `chmod u+rwx,g+r-x,o-rwx <file>` : full access to user, provide read access to the group and remove exeecution. and remove all permission for others
- `chmod ugo+rx <file>` give read and execute permission to user, group and other's 
- to change group of the file `chown owner:group file` or `chgrp group file`


---
## SCP
- `scp -pr <source> <destination>` : - `r` for recursivly copy the directory of the files, `-p` for preserving permission. destination `host:/home/user`


 
## iptables
- `iptables -L` : for listing out rules
- `iptables -A INPUT -p tcp -d 172.16.238.187 --dport 22 -j ACCEPT`:
accept incoming traffic from ip adress via port 22 protocol tcp
- `ip a` to list ip address
- `ip r` for gateway config
- `ip link` for list of all network interfaces
- `nslookup <adress>`for checking the address
- `traceroute <address>` for tracing routes taken by the packet 



## cron
- `crontab -e` to edit cron job
- `crontab -l`
- `tail /var/log/syslog` for checking syslogs


---

## service via systemd
-   to create service for a script test.sh
    ```
    /etc/systemd/system/test.service : 
    [Service]
    ExecStart= /bin/bash /usr/bin/test.sh
    ```
- `systemctl start test.service` : starting a service
- `systemctl status test.service` : status of a service
- `systemctl stop test.service` : starting a service
- `systemctl daemo-reload`  reload sys mngmt service

|command | usagae|
|---|----|
|enable | enable of service after boot up|
|reload | reload of service|


- `journalctl` : list logs with systemd cmd
- `journalctl -b` : list logs with systemd cmd for the current boot
- `journalctl -u docker.service` : list problems with a specific service

