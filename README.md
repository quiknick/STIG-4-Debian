# STIG-4-Debian

##About

This scrpit is use check DISA STIG(Security Technical Implementation Guides) for Debian 8
Porting from DISA RHEL 6 STIG V1 R7.

[DISA RHEL 6 STIG V1 R7](http://iase.disa.mil/stigs/os/unix-linux/Pages/red-hat.aspx)


##Usage

```
#bash check.sh
usage: check.sh [options]

  -c    Output Log with catable colors
  -s    Perform STIG checking with NORMAL output log
  -v    Show version
  -h 	Show this message

Default log file location at /var/log/STIG-Checking-*.log

STIG Check for Debian (v0.1)

Port DISA RHEL 6 STIG V1R7 for Debian
```

##Porting log


RHEL-06-000008: Vendor-provided cryptographic certificates must be installed to verify the integrity of system software.
Change corresponding gpg key check to Debian compatible.

RHEL-06-000011: System security patches and updates must be installed and up-to-date.
Change corresponding update utility to Debian compatible.

RHEL-06-000017: The system must use a Linux Security Module at boot time.
Change the SElinux to AppArmor

RHEL-06-000030: The system must not have accounts configured with blank or null passwords.
Change /etc/pam.d/system-auth - CentOS/RHEL/Fedora/Red Hat/Scientific Linux pam config file.
To /etc/pam.d/common-password - Debian / Ubuntu Linux pam config file.
For more Detial http://www.cyberciti.biz/tips/linux-or-unix-disable-null-passwords.html

RHEL-06-000061:The system must disable accounts after three consecutive unsuccessful logon attempts.
Change pam_faillock.so pam module to use pam_tally2.so

RHEL-06-000065:The system boot loader configuration file(s) must be owned by root.
RHEL-06-000066:The system boot loader configuration file(s) must be group-owned by root.
RHEL-06-000067:The system boot loader configuration file(s) must have mode 0600 or less permissive.
Change /etc/grub.conf to /boot/grub/grub.cfg

RHEL-06-000068:The system boot loader must require authentication.
Change grub-crypt --sha-512 to grub-mkpasswd-pbkdf2 

RHEL-06-000069:The system must require authentication upon booting into single-user and maintenance modes.
DEPRECATED.Debian and therefore Ubuntu both require root password when booting into single user mode or recovery mode. RHEL and CentOS allows access from the console into single user mode without a password.

RHEL-06-000070:The system must not permit interactive boot.
DEPRECATED.Don't find any interactive boot option in debian yet.

RHEL-06-000073:The Department of Defense (DoD) login banner must be displayed immediately prior to, or as part of, console login prompts.
DEPRECATED

RHEL-06-000079:The system must limit the ability of processes to have simultaneous write and execute access to memory.
In debian 8 amd64, system enabled NX by default,and debian 8 i386 system use PAE by default

RHEL-06-000098:The IPv6 protocol handler must not be bound to the network stack unless needed.
Change ipv6 checking method and disable method.
Use /proc/net/if_inet6 to check if ipv6  is enabled
Use kernel boot option in Grub "ipv6.disable=1" to disable ipv6 permanently

RHEL-06-000103:The system must employ a local IPv6 firewall.
RHEL-06-000106:The operating system must connect to external networks or information systems only through managed IPv6 interfaces consisting of boundary protection devices arranged in accordance with an organizational security architecture.
RHEL-06-000107:The operating system must prevent public IPv6 access into an organizations internal networks,except as appropriately mediated by managed interfaces employing boundary protection devices.
RHEL-06-000113:The system must employ a local IPv4 firewall.
RHEL-06-000116:The operating system must connect to external networks or information systems only through managed IPv4 interfaces consisting of boundary protection devices arranged in accordance with an organizational security architecture.
RHEL-06-000117:The operating system must prevent public IPv4 access into an organizations internal networks, except as appropriately mediated by managed interfaces employing boundary protection devices.
DEPRECATED. Debian 8 enable iptables (both ipv4 and ipv6) by default

RHEL-06-000183:The audit system must be configured to audit modifications to the systems Mandatory Access Control (MAC) configuration (SELinux).
Change SELinux to Apparmor

RHEL-06-000203:The xinetd service must be disabled if no network services utilizing it are enabled.
Using 'service --status-all | grep "xinetd" ' instead of chkconfig

RHEL-06-000211:The telnet daemon must not be running.
Using 'service --status-all | grep "telnetd" ' instead of chkconfig

RHEL-06-000214:The rshd service must not be running.
The rshd service in debian using xinetd, so use "xinetd" to check if service is running

RHEL-06-000240:The SSH daemon must be configured with the Department of Defense (DoD) login banner.
DEPRECATED

RHEL-06-000247:The system clock must be synchronized continuously, or at least daily.
In debian use ntp instead of ntpd

RHEL-06-000248:The system clock must be synchronized to an authoritative DoD time source.
Changing `DoD` time source to trusted time source 

RHEL-06-000261:The Automatic Bug Reporting Tool (abrtd) service must not be running.
DEPRECATED.
Didn't find abrtd-like  tool in debian yet

RHEL-06-000266:The oddjobd service must not be running.
DEPRECATED.Debian don't have oddjob service or package

RHEL-06-000267:The qpidd service must not be running.
Debian don't have qpidd service by default

RHEL-06-000268:The rdisc service must not be running.
Debian don't have rdisc service by default

##Project Work

* Up to RHEL-06-201 and still working on what's left
