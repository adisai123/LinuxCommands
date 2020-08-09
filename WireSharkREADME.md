# filter:
```
tcp.flags.push == 1  # to get data packet

ip.dsfield.dscp != 0 

ip.addr eq 192.168.25.200 and ip.addr eq 192.168.25.50

tcp.flags.ack ==1 and tcp.flags.syn == 1

frame contains "QHTTP"    # capture frame contents

```

Protocol list:
IP
UDP
HTTP
TCp

ICMP
NBSS protocol (windows use between lan communication)
