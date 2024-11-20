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

## IF YOU SEE PORT 80 or 8080 JUST NAVIGATE TO WEBPAGE DO NOT wget

# Crete multiple port forwards in one command

(CANNOT FORWARD 6666 or 4444)

```
ssh -S /tmp/jump jump -O forward -L1111:192.168.28.100:80 -L2222:192.168.28.100:2222 -L3333:192.168.28.111:80 -L5555:192.168.28.111:2222
```

ss -ntlp to verify ports, All PIDS should be the same

# Navigate to those webpages

	firefox
 In url bar

 	127.0.0.1:1111

  Loopback to local port connecting to remote httpexit

# ***SIM***
  # Authenticate to first Target using new master socket w/credentials

  	ssh -MS /tmp/t1 creds@127.0.0.1 -p 2222

# ping sweep new network

	for i in {20..40}; do (ping -c 1 100.200.25.$i | grep "bytes from" &) ; done

### found 100.200.25.30,35

## cancel first port forward

	ssh -S /tmp/jump -O close -D9050

(To close change "forward" to "cancel")
 
# port forward through new master socket t1

	ssh -S /tmp/t1 -O forward -D9050

# scan found IPs

	proxychains nmap 10.200.25.30,35

### found 80 and 2222 on both

## interrogate found ports 

proxychains nc 100.200.25.30[35] 80[2222]

# New port forward
	ssh -S /tmp/t1 t1 -O forward -L7777:200.100.25.30:80 -L8888:200.100.25.30:2222 -L9999:200.100.25.35:80 -L1112:200.100.25.35:2222


# New Master Socket using ports we just created

	ssh -MS /tmp/t2 creds@127.0.0.1 -p 1112

# ***END SIM***


