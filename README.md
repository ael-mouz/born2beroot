# born2beroot

## Setup SSH

[How to Enable SSH](https://phoenixnap.com/kb/how-to-enable-ssh-on-debian)

[How to Change SSH Port](https://www.ubuntu18.com/ubuntu-change-ssh-port/)

[Enable or disable remote root login](https://www.ibm.com/docs/en/db2/11.5?topic=installation-enable-disable-remote-root-login)

1-Install ssh
```bash
$ sudo apt install openssh-server
$ sudo apt-get install openssh-client
```
2-Change port ssh ```add the following line```
```bash
$ sudo nano /etc/ssh/sshd_config
    port 4242
```
3-Disable remote root login ```add the following line```
```bash
$ sudo nano /etc/ssh/sshd_config
    PermitRootLogin no
```
4-Check the status of the SSH service
```bash
$ sudo systemctl status ssh

or

$ sudo service ssh status
```
5-Enable or start the SSH service
```bash
$ sudo systemctl enable ssh

or

$ sudo service ssh start
```
6-Disable or stop the SSH service
```bash
$ sudo systemctl disable ssh

or

$ sudo service ssh stop
```
7-Restart the SSH service
```bash
$ sudo systemctl restart ssh

or

$ sudo service ssh restart
```
8-Connect to server
```bash
$ ssh username@host -p [port]
```
    
## UFW

(https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-debian-9)

```bash
    sudo apt install ufw
```
```bash
    sudo ufw allow ssh
```
```bash
    sudo ufw allow [port]
```
```bash
    sudo ufw enable
```
```bash
    sudo ufw disable
```
```bash
    sudo ufw reset
```
```bash
    sudo ufw status numbered
```
```bash
    sudo ufw delete [number]
```

## HOSTNAME

(https://www.cyberciti.biz/faq/debian-change-hostname-permanently/)

```bash
    hostnamectl set-hostname [machine-name-here]
```
```bash
    hostname
```
```bash
    nano /etc/hosts
        127.0.0.1 [hostname]
```
```bash
    nano /etc/hostname
        [hostname]
```

## SUDO

(https://phoenixnap.com/kb/how-to-create-sudo-user-on-ubuntu)

(https://www.digitalocean.com/community/tutorials/how-to-add-delete-and-grant-sudo-privileges-to-users-on-a-debian-vps)

```bash
apt-get install sudo
```
```bash
adduser [username]
```
```bash
adduser [username] sudo
```
```bash
usermod -aG sudo [username]
```
```bash
deluser --remove-home [username]
```
```bash
su - newuser
```

---

(https://linuxize.com/post/how-to-create-groups-in-linux/)

```bash
groupadd mygroup
```
```bash
getent group
```
```bash
getent group [username]
```
```bash
sudo groupdel [group-name-here]
```

---

(https://www.tecmint.com/sudoers-configurations-for-setting-sudo-in-linux/)

```bash
    nano /etc/sudoers
        Defaults    passwd_tries=3
        Defaults    badpass_message="Password is wrong, please try again"
        Defaults    logfile="/var/log/sudo/sudo.log"
        Defaults    log_input, log_output
        Defaults    requiretty
        Defaults    secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

## PASSWORD

(https://www.redhat.com/sysadmin/password-expiration-date-linux)

```bash
    nano /etc/login.defs
        PASS_MAX_DAYS   30
        PASS_MIN_DAYS   2
        PASS_WARN_AGE   7
```
```bash
    sudo chage -M 30 -m 2 -w 7 [username]
```
```bash
    sudo chage -l [username]
```

---

(https://ostechnix.com/how-to-set-password-policies-in-linux/)

(https://www.xmodulo.com/set-password-policy-linux.html)

(https://computingforgeeks.com/enforce-strong-user-password-policy-ubuntu-debian/)

(https://www.stigviewer.com/stig/red_hat_enterprise_linux_6/2020-09-03/finding/V-218047)

```bash
    sudo apt-get -y install libpam-pwquality cracklib-runtime
```
```bash
    nano /etc/pam.d/common-password
        password    requisite   pam_pwquality.so retry=3 minlen=10 dcredit=-1 ucredit=-1 lcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
```
```bash
    sudo passwd [username]
```

## SCRIPT MONITORING

(https://linuxize.com/post/wall-command-in-linux/

(https://vitux.com/how-to-get-hardware-details-in-debian-11/

(https://www.cyberciti.biz/faq/check-how-many-cpus-are-there-in-linux-system/

(https://phoenixnap.com/kb/free-linux-command#:~:text=The%20Linux%20free%20command%20outputs,the%20free%20command%20in%20Linux.

(https://www.redhat.com/sysadmin/Linux-df-command#:~:text=The%20df%20command%20displays%20the,with%20each%20file%20name's%20argument.

(https://www.geeksforgeeks.org/mpstat-command-in-linux-with-examples/

(https://www.javatpoint.com/who-command-in-linux#:~:text=The%20Linux%20%22who%22%20command%20lets,command%20to%20get%20that%20information.

(https://www.digitalocean.com/community/tutorials/if-else-in-shell-scripts

(https://www.redhat.com/sysadmin/netstat#:~:text=The%20network%20statistics%20(%20netstat%20)%20command,common%20uses%20for%20this%20command.

(https://devconnected.com/how-to-list-users-and-groups-on-linux/#:~:text=In%20order%20to%20list%20users,navigate%20within%20the%20username%20list.

(https://www.geeksforgeeks.org/hostname-command-in-linux-with-examples/

(https://unix.stackexchange.com/questions/167935/details-about-sudo-commands-executed-by-all-user

```
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

(https://vitux.com/how-to-setup-a-cron-job-in-debian-10/)

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

