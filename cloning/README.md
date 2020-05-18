With progress
--
1. run: `dd if=/dev/sda of=/dev/sdb bs=1024k status=progress`


With compression
--
1. run: `dd if=/dev/sda conv=sync,noerror bs=1024k status=progress | gzip -c > ~/images/octopi4.image.gz`


Write to disk
--
Just use etcher...


Change hostname
--
1. Edit both `/etc/hosts` and `/etc/hostname` or use `sudo raspi-config` > `hostname`


Change Static IP
--
1. Install nmap: `sudo apt-get install -y nmap`
1. Check for available static ips: `nmap -sP 192.168.1.1/24 | grep -i Nmap | sed 's/^Nmap scan report for //'`
1. Edit `sudo vim /etc/dhcpcd.conf` and change the relevant static ips


References
--
1. [https://www.cyberciti.biz/faq/how-to-create-disk-image-on-mac-os-x-with-dd-command/](https://www.cyberciti.biz/faq/how-to-create-disk-image-on-mac-os-x-with-dd-command/)xs