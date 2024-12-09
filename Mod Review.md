# Recon(Nmap,PING)

Interrogate Ports

nmap --script=hhtp-enum

Don't immediately wget -r, port forward and interface 

Robots.txt

SQL INJECT VUL FIELDS

;whoami

    inhert permissions and plant .ssh rsa key

Authentication bypass

Once ssh key uploaded

Win (Auditpol) Admin Only, Escalate Privs

Lin (ps -elf/top/htop/crontab)

# Binary Analysis
Static analysis

        Strings
        File

Dynamic Analysis

    Run and interact with .exe

Open Ghidra 

    Looking for running strings
    Once string is found click it and see values associated

```
if x >> 4=32 {
    code
}
```
Midshifting

    Shifting bits to the left

x would need to equal 512 in order to make statement true

x >> 4=32

00 0010 0000 (32)

32 << 4 =x

10 0000 0000 (512)

x = 512


# Post Ex

## Windows Perst.

HKLM RUN KEYS

Run Once

## Win Priv Esc

.exe renaming

.dll highjacking

Check Task Scheduler and Services for goofy shit

## Lin 

cat /etc/passwd

cat /etc/hosts

sudo -l 

ps -elf

/home*

find suid/guid cmd

gtfobins

## To look at functions

disass func













