# Master Socket
Establish tcp connections to other boxes in net

	ssh -MS /tmp/jump student@10.50.29.13

	pass: 3wyq2y7ZBd2ffkB

# ONLY COMMAND RAN ON JUMP

	for i in {1..254}; do (ping -c 1 192.168.65.$i | grep "bytes from" &) ; done

 ## Output
```
64 bytes from 192.168.28.97: icmp_seq=1 ttl=64 time=1.31 ms
64 bytes from 192.168.28.100: icmp_seq=1 ttl=63 time=3.87 ms
64 bytes from 192.168.28.99: icmp_seq=1 ttl=63 time=3.40 ms
64 bytes from 192.168.28.105: icmp_seq=1 ttl=63 time=0.948 ms
64 bytes from 192.168.28.98: icmp_seq=1 ttl=63 time=16.2 ms
64 bytes from 192.168.28.111: icmp_seq=1 ttl=63 time=1.01 ms
64 bytes from 192.168.28.120: icmp_seq=1 ttl=63 time=0.969 ms
```

# Set Up Dynamic Port Forward TO Jump from Lin_Ops

	ssh -S /tmp/jump jump -O forward -D9050

-S tells ssh we're using a socket file

-O (Not 0) indicates copntrol options

	ss -ntlp

 To verify its running, output should include 

 	127.0.0.1:9050

# nmap ips dicovered in ping sweep

	proxychains nmap 192.168.28.100,111

## Output of nmap
```
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1

Nmap scan report for 192.168.28.111
Host is up (0.00077s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE
80/tcp   open  http
2222/tcp open  EtherNetIP-1
8080/tcp open  http-proxy
```
# Verify ports associated with service

	proxychains nc 192.168.28.111 2222

## IF YOU SEE 80 or 8080 JUST NAVIGATE TO WEBPAGE DO NOT wget
 

ssh -S /tmp/jump jump -O forward -L1111:192.168.28.100:80 -L2222:192.168.28.100:2222 -L3333:192.168.28.111:80 
 -L4444:192.168.28.111:2222







 
