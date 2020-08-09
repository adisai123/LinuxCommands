# filter:
```
tcp.flags.push == 1  # to get data packet

ip.dsfield.dscp != 0 

ip.addr eq 192.168.25.200 and ip.addr eq 192.168.25.50

tcp.flags.ack ==1 and tcp.flags.syn == 1   #list of ports

frame contains "QHTTP"    # capture frame contents

tcp.port == 80 || udp.port == 80

```

```
Discover live system 
nmap port options (find numer of open ports)
 -nS , -nT, -nT
nmap -sP  subnetip

scan perticular port :
aditya@aditya-nupur:~$ sudo nmap -sS -p 7070 192.168.43.196 

service scap :
nmap -sV  192.168.43.196 

Enumeration scan
nmap -A -p 7070 192.168.43.196

```

Protocol list:
IP
UDP
HTTP
TCp

ICMP
NBSS protocol (windows use between lan communication)
