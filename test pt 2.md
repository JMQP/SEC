www-data@ministry-defense-11:~$ for i in {1..254}; do (ping -c 1 192.168.28.$i | grep "bytes from" &) ; done
64 bytes from 192.168.28.5: icmp_seq=1 ttl=127 time=1.36 ms
64 bytes from 192.168.28.10: icmp_seq=1 ttl=63 time=1.49 ms
64 bytes from 192.168.28.19: icmp_seq=1 ttl=63 time=1.28 ms
64 bytes from 192.168.28.30: icmp_seq=1 ttl=64 time=0.430 ms
64 bytes from 192.168.28.177: icmp_seq=1 ttl=63 time=11.7 ms
64 bytes from 192.168.28.182: icmp_seq=1 ttl=63 time=1.23 ms
64 bytes from 192.168.28.190: icmp_seq=1 ttl=64 time=0.199 ms


Nmap scan report for 192.168.28.5
Host is up (0.00076s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
9999/tcp open  abyss

Nmap scan report for 192.168.28.10
Host is up (0.00076s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh

Nmap scan report for 192.168.28.19
Host is up (0.00077s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh


RSANCH WORKS ON WIN port 1112

KMICHAE WORKS ON r-and-d-nix2 port 1113

MSMITH WORKS ON RNDNIX1 port 1114



# MSmith@r-and-d-nix1

 find / -type f -perm /6000 -ls 2>/dev/null # Find SUID and/or SGID files
     6532     12 -rwxr-sr-x   1 root     utmp        10232 Mar 11  2016 /usr/lib/x86_64-linux-gnu/utempter/utempter
     6493    100 -rwsr-xr-x   1 root     root       100760 Nov 23  2018 /usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
    12442    428 -rwsr-xr-x   1 root     root       436552 Mar  4  2019 /usr/lib/openssh/ssh-keysign
     7930     44 -rwsr-xr--   1 root     messagebus    42992 Jun 10  2019 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
     8026    108 -rwsr-sr-x   1 root     root         109432 Oct 30  2019 /usr/lib/snapd/snap-confine
     7934     12 -rwsr-xr-x   1 root     root          10232 Mar 28  2017 /usr/lib/eject/dmcrypt-get-device
     8020     16 -rwsr-xr-x   1 root     root          14328 Mar 27  2019 /usr/lib/policykit-1/polkit-agent-helper-1
     4341     76 -rwsr-xr-x   1 root     root          75824 Mar 22  2019 /usr/bin/gpasswd
     4337     72 -rwxr-sr-x   1 root     shadow        71816 Mar 22  2019 /usr/bin/chage
     4342     60 -rwsr-xr-x   1 root     root          59640 Mar 22  2019 /usr/bin/passwd
     4303     40 -rwxr-sr-x   1 root     crontab       39352 Nov 16  2017 /usr/bin/crontab
     4340     24 -rwxr-sr-x   1 root     shadow        22808 Mar 22  2019 /usr/bin/expiry
     4499     44 -rwxr-sr-x   1 root     mlocate       43088 Mar  1  2018 /usr/bin/mlocate
     4507    356 -rwxr-sr-x   1 root     ssh          362640 Mar  4  2019 /usr/bin/ssh-agent
     4648     40 -rwsr-xr-x   1 root     root          37136 Mar 22  2019 /usr/bin/newuidmap
     4339     44 -rwsr-xr-x   1 root     root          44528 Mar 22  2019 /usr/bin/chsh
     4140     40 -rwsr-xr-x   1 root     root          40344 Mar 22  2019 /usr/bin/newgrp
     4338     76 -rwsr-xr-x   1 root     root          76496 Mar 22  2019 /usr/bin/chfn
     4400     16 -rwxr-sr-x   1 root     tty           14328 Jan 17  2018 /usr/bin/bsd-write
     4539     52 -rwsr-sr-x   1 daemon   daemon        51464 Feb 20  2018 /usr/bin/at
     4659     24 -rwsr-xr-x   1 root     root          22520 Mar 27  2019 /usr/bin/pkexec
     4058     32 -rwxr-sr-x   1 root     tty           30800 Jan  8  2020 /usr/bin/wall
     4495     20 -rwsr-xr-x   1 root     root          18448 Jun 28  2019 /usr/bin/traceroute6.iputils
     4099     36 -rwsr-xr-x   1 root     root          35000 Jan 18  2018 /usr/bin/nice
     4647     40 -rwsr-xr-x   1 root     root          37136 Mar 22  2019 /usr/bin/newgidmap
     4261    148 -rwsr-xr-x   1 root     root         149080 Jan 31  2020 /usr/bin/sudo
     3823     36 -rwxr-sr-x   1 root     shadow        34816 Feb 27  2019 /sbin/unix_chkpwd
     3819     36 -rwxr-sr-x   1 root     shadow        34816 Feb 27  2019 /sbin/pam_extrausers_chkpwd
      139     32 -rwsr-xr-x   1 root     root          30800 Aug 11  2016 /bin/fusermount
       56     44 -rwsr-xr-x   1 root     root          43088 Jan  8  2020 /bin/mount
      109     64 -rwsr-xr-x   1 root     root          64424 Jun 28  2019 /bin/ping
       55     44 -rwsr-xr-x   1 root     root          44664 Mar 22  2019 /bin/su
       57     28 -rwsr-xr-x   1 root     root          26696 Jan  8  2020 /bin/umount

## rysylog.conf 

 UDP, 192.168.28.199 £ i5fzgprBLOprk6HeTS7i


## £ find / -iname "*password*" 2>/dev/null
/etc/pam.d/common-password
/var/cache/debconf/passwords.dat
/var/lib/pam/password
/var/lib/cloud/instances/iid-datasource-none/sem/config_set_passwords
/run/systemd/ask-password
/boot/grub/i386-pc/password.mod
/boot/grub/i386-pc/legacy_password_test.mod
/boot/grub/i386-pc/password_pbkdf2.mod
/boot/grub/x86_64-efi/password.mod
/boot/grub/x86_64-efi/legacy_password_test.mod
/boot/grub/x86_64-efi/password_pbkdf2.mod
/usr/share/perl5/Debconf/Element/Kde/Password.pm
/usr/share/perl5/Debconf/Element/Editor/Password.pm
/usr/share/perl5/Debconf/Element/Noninteractive/Password.pm
/usr/share/perl5/Debconf/Element/Dialog/Password.pm
/usr/share/perl5/Debconf/Element/Web/Password.pm
/usr/share/perl5/Debconf/Element/Gnome/Password.pm
/usr/share/perl5/Debconf/Element/Teletype/Password.pm
/usr/share/pam/common-password.md5sums
/usr/share/pam/common-password
/usr/share/man/man1/systemd-ask-password.1.gz
/usr/share/man/man1/systemd-tty-ask-password-agent.1.gz
/usr/share/man/man8/systemd-ask-password-console.service.8.gz
/usr/share/man/man8/systemd-ask-password-wall.service.8.gz
/usr/share/man/man8/systemd-ask-password-wall.path.8.gz
/usr/share/man/man8/systemd-ask-password-console.path.8.gz
/usr/lib/python3/dist-packages/oauthlib/oauth2/rfc6749/grant_types/__pycache__/resource_owner_password_credentials.cpython-36.pyc
/usr/lib/python3/dist-packages/oauthlib/oauth2/rfc6749/grant_types/resource_owner_password_credentials.py
/usr/lib/python3/dist-packages/cloudinit/config/cc_set_passwords.py
/usr/lib/python3/dist-packages/cloudinit/config/__pycache__/cc_set_passwords.cpython-36.pyc
/usr/lib/grub/i386-pc/password.mod
/usr/lib/grub/i386-pc/legacy_password_test.mod
/usr/lib/grub/i386-pc/password_pbkdf2.mod
/usr/lib/grub/x86_64-efi/password.mod
/usr/lib/grub/x86_64-efi/legacy_password_test.mod
/usr/lib/grub/x86_64-efi/password_pbkdf2.mod
/lib/systemd/system/multi-user.target.wants/systemd-ask-password-wall.path
/lib/systemd/system/systemd-ask-password-wall.path
/lib/systemd/system/systemd-ask-password-wall.service
/lib/systemd/system/systemd-ask-password-plymouth.path
/lib/systemd/system/systemd-ask-password-console.service
/lib/systemd/system/systemd-ask-password-console.path
/lib/systemd/system/sysinit.target.wants/systemd-ask-password-console.path
/lib/systemd/system/systemd-ask-password-plymouth.service
/lib/systemd/systemd-reply-password
/lib/libhanbles/Passwords.txt
/bin/systemd-tty-ask-password-agent
/bin/systemd-ask-password
