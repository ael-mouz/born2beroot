
# born2beroot

## Setup SSH

[Enable SSH](https://phoenixnap.com/kb/how-to-enable-ssh-on-debian)

[Change SSH Port](https://www.ubuntu18.com/ubuntu-change-ssh-port/)

[Enable or disable remote root login](https://www.ibm.com/docs/en/db2/11.5?topic=installation-enable-disable-remote-root-login)

---
\
1.Install ssh
```bash
	$ sudo apt install openssh-server
	$ sudo apt-get install openssh-client
```
2.Change port ssh `add the following line`
```bash
	$ sudo nano /etc/ssh/sshd_config
		port 4242
```
3.Disable remote root login `add the following line`
```bash
	$ sudo nano /etc/ssh/sshd_config
		PermitRootLogin no
```
4.Check the status of the SSH service
```bash
	$ sudo systemctl status ssh
```
```bash
	$ sudo service ssh status
```
5.Enable or start the SSH service
```bash
	$ sudo systemctl enable ssh
```
```bash
	$ sudo service ssh start
```
6.Disable or stop the SSH service
```bash
	$ sudo systemctl disable ssh
```
```bash
	$ sudo service ssh stop
```
7.Restart the SSH service
```bash
	$ sudo systemctl restart ssh
```
```bash
	$ sudo service ssh restart
```
8.Connect to server
```bash
	$ ssh username@host -p [port]
```
	
## UFW

[Set Up a Firewall with UFW](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-debian-9)

---
\
1.Install UFW
```bash
	$ sudo apt install ufw
```
2.Allow UFW port
```bash
	$ sudo ufw allow [port]
```
3.Enble UFW service
```bash
	$ sudo ufw enable
```
4.Disable UFW service
```bash
	$ sudo ufw disable
```
5.Reset UFW service
```bash
	$ sudo ufw reset
```
6.Check open port of the UFW service
```bash
	$ sudo ufw status numbered
```
7.Delete UFW port
```bash
	$ sudo ufw delete [number]
```

## HOSTNAME

[Change Hostname / Computer Name Permanently](https://www.cyberciti.biz/faq/debian-change-hostname-permanently/)

---
\
1.Show the hostname
```bash
	$ hostname
```
2.Change Hostname
```bash
	$ sudo hostname [machine-name-here]
```
3.Change Hostname permanently
```bash
	$ sudo hostnamectl set-hostname [machine-name-here]
```
4.Change the hostname by Edit the file `/etc/hostname`
```bash
	$ sudo nano /etc/hostname
		[hostname]
```
5.Change the hostname by Edit the file `/etc/hosts`
```bash
	$ sudo nano /etc/hosts
		127.0.0.1 [hostname]
```

## SUDO

[Add User To Sudoers & Add User To Sudo Group](https://phoenixnap.com/kb/how-to-create-sudo-user-on-ubuntu)

[Add, Delete, and Grant Sudo Privileges to Users](https://www.digitalocean.com/community/tutorials/how-to-add-delete-and-grant-sudo-privileges-to-users-on-a-debian-vps)

[Create Groups](https://linuxize.com/post/how-to-create-groups-in-linux/)

[Useful Sudoers Configurations](https://www.tecmint.com/sudoers-configurations-for-setting-sudo-in-linux/)

---
### Set up sudo
\
1.Install sudo
```bash
	$ apt-get install sudo
```
2.Create user
```bash
	$ sudo adduser [username]
```
3.Add user to sudo group && Grant privileges
```bash
	$ sudo adduser [username] sudo
```
```bash
	$ sudo usermod -aG sudo [username]
```
4.Delete user
```bash
	$ sudo deluser --remove-home [username]
```
5.Switch to another user
```bash
	$ su - newuser
```
---
---
---
### Create Groups
\
1.Create group
```bash
	$ sudo groupadd [mygroup]
```
2.Show group
```bash
	$ sudo getent group 
```
3.Show group Users
```bash
	$ sudo getent group [username]
```
4.Delete group
```bash
	$ sudo groupdel [group-name-here]
```
---
---
---
### Sudoers Configurations
\
1.Add this lines to `visudo` or `/etc/sudoers`
```bash
	$ sudo nano /etc/sudoers
		Defaults    passwd_tries=3
		Defaults    badpass_message="Password is wrong, please try again"
		Defaults    logfile="/var/log/sudo/sudo.log"
		Defaults    log_input, log_output
		Defaults    requiretty
		Defaults    secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

## PASSWORD

[Set user password expirations](https://www.redhat.com/sysadmin/password-expiration-date-linux)

[Set Password policy 1](https://ostechnix.com/how-to-set-password-policies-in-linux/)

[set password policy 2](https://www.xmodulo.com/set-password-policy-linux.html)

[set password policy 3](https://computingforgeeks.com/enforce-strong-user-password-policy-ubuntu-debian/)

[set password policy 4](https://access.redhat.com/discussions/1265203)

---
### User password expiration
\
1.Edit this lines on `/etc/login.defs`
```bash
	$ sudo nano /etc/login.defs
		PASS_MAX_DAYS   30
		PASS_MIN_DAYS   2
		PASS_WARN_AGE   7
```
2.Change the password expiration for a user
```bash
	$ sudo chage -M 30 -m 2 -w 7 [username]
```
3.Show the password expiration of a user
```bash
	$ sudo chage -l [username]
```
---
---
---
### password policy
\
1.Install this library
```bash
	$ sudo apt-get -y install libpam-pwquality cracklib-runtime
```
2.Add the line below to `/etc/pam.d/common-password`
```bash
	$ sudo nano /etc/pam.d/common-password
		password    requisite   pam_pwquality.so retry=3 minlen=10 dcredit=-1 ucredit=-1 lcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
```
3.Chnage password
```bash
	$ sudo passwd [username]
```

## SCRIPT MONITORING

[Wall command](https://linuxize.com/post/wall-command-in-linux/)

[Get System and Hardware Details with uname](https://vitux.com/how-to-get-hardware-details-in-debian-11/)

[check how many CPUs are there in Linux system](https://www.cyberciti.biz/faq/check-how-many-cpus-are-there-in-linux-system/)

[Using the Linux free Command](https://phoenixnap.com/kb/free-linux-command)

[Check your disk space use with the Linux df command](https://www.redhat.com/sysadmin/Linux-df-command)

[mpstat Command in Linux](https://www.geeksforgeeks.org/mpstat-command-in-linux-with-examples/)

[Who command in Linux](https://www.javatpoint.com/who-command-in-linux)

[if-else in Shell Scripts](https://www.digitalocean.com/community/tutorials/if-else-in-shell-scripts)

[Linux networking: netstat](https://www.redhat.com/sysadmin/netstat)

[List Users on Linux](https://devconnected.com/how-to-list-users-and-groups-on-linux/)

[hostname command in Linux](https://www.geeksforgeeks.org/hostname-command-in-linux-with-examples/)

[Details about sudo commands executed by all user](https://unix.stackexchange.com/questions/167935/details-about-sudo-commands-executed-by-all-user)

[Understanding Physical and Logical CPUs](https://www.linkedin.com/pulse/understanding-physical-logical-cpus-akshay-deshpande/)

[Setup a Cron Job](https://vitux.com/how-to-setup-a-cron-job-in-debian-10/)

---
\
1.Create a script named `monitoring.sh`
```bash
#!/bin/bash
arch=$(uname -a)
cpu=$(nproc)
vcpu=$(lscpu | grep 'Core(s)' | awk '{print $4}')
memu1=$(free -m | grep Mem | awk '{print $3 "/" $2 "MB"}')
memu2=$(free | grep Mem | awk '{printf("%.2f"), $3/$2*100}')
disku=$(df -h --total | grep total | awk '{print $3 "/" $2 " " "("$5")"}')
cpul=$(mpstat | grep 'all' | awk '{print 100 -  $13 "%"}')
boot=$(who -b | awk '{print $3 " " $4}')
n=$(lsblk | awk '{print $6}' | grep lvm | wc -l)
lvm=$(if [ $n -gt 0 ]; then echo yes; else echo no; fi)
tcp=$(netstat | grep "tcp.*ESTABLISHED" | wc -l)
userl=$(users | sort | uniq | wc -l)
ip1=$(hostname -I)
ip2=$(ip address | grep 'ether '| awk '{ print $2}')
sudo=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
wall "
		#Architectur: $arch
		#CPU physical: $cpu
		#vCPU : $vcpu
		#Memory Usage: $memu1 ($memu2%)
		#Disk Usage: $disku
		#CPU load: $cpul
		#Last boot: $boot
		#LVM use: $lvm
		#Connections TCP : $tcp ESTABLISHED
		#User log: $userl
		#Network: IP $ip1 ($ip2)
		#Sudo : $sudo cmd
"
```
---



```
sudo crontab -e
```
```
sudo crontab -l
```
```
sudo crontab -r
```

## BONUS

(https://geekrewind.com/install-wordpress-on-ubuntu-16-04-lts-with-lighttpd-mariadb-and-php-7-1-support/)


(https://www.atlantic.net/dedicated-server-hosting/how-to-install-wordpress-with-lighttpd-web-server-on-ubuntu-20-04/)


(https://www.osradar.com/install-wordpress-with-lighttpd-debian-10/)


https://www.tecmint.com/install-lighttpd-in-ubuntu/
