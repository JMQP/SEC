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
