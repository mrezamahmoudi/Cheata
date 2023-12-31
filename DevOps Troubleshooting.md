# System Load

#### 5; 10; 15 minute CPU load average
> uptime

#### (b)atch mode; (n)times to update before closing
> top -b -n 1

#### /etc/d­efa­ult­/sy­sstat 'ENABL­ED=­"­tru­e"'
> systat pkg

#### top, but for disk usage
> iotop

#### shows I/O stats for blk devices.
> iostat

#### view sysstat logs for the day
> sar

#### -r View ram statistic ; -b view I/O statistics
> sar (-r) (-b)

#### view stats within range date (s)tart to (e)nd
> sar -s 00:00:00 -e 00:00:00

#### from full path
> sar -f /var/l­og/­sys­sta­t/sa**


# Disk Management

#### Change the label on a ext* filesystem

> e2label /dev/sd* /
#### locate­/print block device attributes

> blkid
#### file systems mounted at boot.

> /etc/fstab
#### Disk Usage (c)Total (k)1k Blk Size (x) one file system. sort by number

> du -ckx | sort -n
#### edit logrotate settings

> /etc/l­ogr­ota­te.conf
#### report disk space usage, (i) inodes

> df -i
#### file system check (y) yes (C) progress bar

> fsck -y -C /dev/sda*
#### list superb­locks on a file system.

> mke2fs -n /dev/sda*
#### run fsck and repair superblock with backup

> fsck -b (super­block) -y -C /dev/sda*


# Networking Troubl­esh­ooting

#### gather inform­ation about network adapters

> ifconfig
#### tool to analyze Ethernet connec­tion.

> ethtool eth0
#### check routing table, (n)o dns resolution

> sudo route -n
#### restart networking service

> sudo service networking restart
#### query dns for URL/IP

> nslookup
#### traces route to host

> traceroute
#### check (p)ort range with $ipaddr

> nmap -p $port $ipaddr
#### show only (l)ist­ening sockets (n)umeric (p)pro­gram, shows PID and name of program

> sudo netstat -lnp
#### Show all firewall rules

> iptables -L
#### top for open network connec­tions

> iftop
#### packet dump

> tcpdump -n
#### filter options for tcpdump

> tcpdump (not) host/port
#### run tcpdump and output to file, -C sets max size of output file

> sudo tcpdump -C 10 -n -l host website | tee outputfile
#### like nslookup, more inform­ative.

> dig website
#### check dns record of target against specific dns

> dig target @dns
#### traces DNS route

> dig target +trace