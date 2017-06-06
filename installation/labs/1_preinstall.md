sudo sysctl vm.swappiness=1
sudo echo "vm.swappiness = 1" >> /etc/sysctl.conf
cat /etc/sysctl.conf

# sysctl settings are defined through files in
# /usr/lib/sysctl.d/, /run/sysctl.d/, and /etc/sysctl.d/.
#
# Vendors settings live in /usr/lib/sysctl.d/.
# To override a whole file, create a new file with the same in
# /etc/sysctl.d/ and put new settings there. To override
# only specific settings, add a file with a lexically later
# name in /etc/sysctl.d/ and put new settings there.
#
# For more information, see sysctl.conf(5) and sysctl.d(5).
vm.swappiness = 1

------------------------------------------------------------

[root@ip-10-0-0-17 ~]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=3985464k,nr_inodes=996366,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,seclabel,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_prio,net_cls)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct,cpu)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
configfs on /sys/kernel/config type configfs (rw,relatime)
/dev/xvda2 on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,relatime)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=32,pgrp=1,timeout=300,minproto=5,maxproto=5,direct)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime,seclabel)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=774732k,mode=700,uid=1000,gid=1000)

------------------------------------------------------------

mount | grep xfs 
/dev/xvda2 on / type xfs (rw,relatime,seclabel,attr2,inode64,noquota)
# XFS so no reserve

------------------------------------------------------------

[root@ip-10-0-0-14 ~]# cat /etc/rc.local 
#!/bin/bash
# THIS FILE IS ADDED FOR COMPATIBILITY PURPOSES
#
# It is highly advisable to create own systemd services or udev rules
# to run scripts during boot instead of using this file.
#
# In contrast to previous versions due to parallel execution during boot
# this script will NOT be run after all other services.
#
# Please note that you must run 'chmod +x /etc/rc.d/rc.local' to ensure
# that this script will be executed during boot.

touch /var/lock/subsys/local
echo 'never' > /sys/kernel/mm/transparent_hugepage/defrag


---------------------------------------------------------
[root@ip-10-0-0-14 ~]# ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP mode DEFAULT qlen 1000
    link/ether 0a:41:68:a9:05:1f brd ff:ff:ff:ff:ff:ff

---------------------------------------------------------


getent hosts ec2-35-176-18-59.eu-west-2.compute.amazonaws.com
getent hosts nslookup 35.176.18.59

35.176.18.59    ec2-35-176-18-59.eu-west-2.compute.amazonaws.com
[ec2-user@ip-10-0-0-14 ~]$ getent hosts ec2-35-176-18-59.eu-west-2.compute.amazonaws.com
10.0.0.14       ec2-35-176-18-59.eu-west-2.compute.amazonaws.com
[ec2-user@ip-10-0-0-14 ~]$ sudo service nscd status
Redirecting to /bin/systemctl status  nscd.service
Unit nscd.service could not be found.
[ec2-user@ip-10-0-0-14 ~]$ sudo - i 
sudo: -: command not found
[ec2-user@ip-10-0-0-14 ~]$ sudo -i
[root@ip-10-0-0-14 ~]# yum install ncsd
Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
rhui-REGION-client-config-server-7                       | 2.9 kB     00:00     
rhui-REGION-rhel-server-releases                         | 3.5 kB     00:00     
rhui-REGION-rhel-server-rh-common                        | 3.8 kB     00:00     
(1/7): rhui-REGION-client-config-server-7/x86_64/primary_d | 1.2 kB   00:00     
(2/7): rhui-REGION-rhel-server-releases/7Server/x86_64/gro | 701 kB   00:00     
(3/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/gr |  104 B   00:00     
(4/7): rhui-REGION-rhel-server-releases/7Server/x86_64/upd | 1.9 MB   00:00     
(5/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/pr | 118 kB   00:00     
(6/7): rhui-REGION-rhel-server-rh-common/7Server/x86_64/up |  33 kB   00:00     
(7/7): rhui-REGION-rhel-server-releases/7Server/x86_64/pri |  36 MB   00:01     
No package ncsd available.

---------------------------------------------------------

yum install ncsd
systemctl start nscd
serivice ncsd start
serivice ncsd status

Redirecting to /bin/systemctl start  nscd.service
[root@ip-10-0-0-14 ~]# systemctl start nscd
[root@ip-10-0-0-14 ~]# service nscd status
Redirecting to /bin/systemctl status  nscd.service
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor preset: disabled)
   Active: active (running) since Tue 2017-06-06 05:53:29 EDT; 1min 33s ago
  Process: 18805 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 18806 (nscd)
   CGroup: /system.slice/nscd.service
           └─18806 /usr/sbin/nscd

Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 mo...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 mo...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 mo...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 mo...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 mo...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 di...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 st...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 Ac...
Jun 06 05:53:29 ip-10-0-0-14.eu-west-2.compute.internal systemd[1]: Started N...
Jun 06 05:53:48 ip-10-0-0-14.eu-west-2.compute.internal nscd[18806]: 18806 ch...
Hint: Some lines were ellipsized, use -l to show in full.


----------------------------------------------------------



yum install ntpdate

Loaded plugins: amazon-id, rhui-lb, search-disabled-repos
Resolving Dependencies
--> Running transaction check
---> Package ntpdate.x86_64 0:4.2.6p5-25.el7_3.2 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package  Arch    Version               Repository                         Size
================================================================================
Installing:
 ntpdate  x86_64  4.2.6p5-25.el7_3.2    rhui-REGION-rhel-server-releases   86 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 86 k
Installed size: 121 k
Is this ok [y/d/N]: y
Downloading packages:
ntpdate-4.2.6p5-25.el7_3.2.x86_64.rpm                      |  86 kB   00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : ntpdate-4.2.6p5-25.el7_3.2.x86_64                            1/1 
  Verifying  : ntpdate-4.2.6p5-25.el7_3.2.x86_64                            1/1 

Installed:
  ntpdate.x86_64 0:4.2.6p5-25.el7_3.2                                           

Complete!


--------------------------------
