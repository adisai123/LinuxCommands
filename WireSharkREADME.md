# Definition
Wireshark is an immensely powerful tool with quite a bit of deep and
complex functionality. It is capable of handling a wide range of known
(and unknown) protocols. But although the functionality range is broad,
most of it aligns to one end: to capture packets and analyze them. Being
able to take the bits and bytes and present them in an organized,
familiar, and human-readable format is what brings people to think of
using Wireshark.

```bash

command to capture packet:
dumpcap -i lo -a duration:60 -w output.pcapng

```

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
```
http.request – Display all HTTP requests.
http.request || http.response – Display all HTTP request and
responses.
ip.addr == 127.0.0.1 – Display all IP packets whose source or
destination is localhost.
tcp.len < 100 – Display all TCP packets whose data length is
less than 100 bytes.
http.request.uri matches “(gif)$” - Display all HTTP requests
in which the uri ends with “gif”.
dns.query.name == “www.google.com” - Display all DNS
queries for “www.google.com”.
```

Protocol list:
IP
UDP
HTTP
TCp

ICMP
NBSS protocol (windows use between lan communication)
