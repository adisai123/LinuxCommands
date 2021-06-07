Remove duplicate record:
```bash
admalpan@ADMALPAN-SNNT5 MINGW64 ~
    $ cat abc.txt
    nupur malpani
    nupur malpani
    aditya malpani
    aditya malpani
    aditya malpani

    admalpan@ADMALPAN-SNNT5 MINGW64 ~
    $ cat abc.txt | sort | uniq > abc.txt ; cat abc.txt
    aditya malpani
    nupur malpani

    admalpan@ADMALPAN-SNNT5 MINGW64 ~
    $
```

to test if port is up :
netstat ,
</dev/127.0.0.1/9002


to start port :
```bash
nc -l 192.168.92.19 <port> -k
```
   
  
Find file n days old 
 to find line with 2 days old
```bash
 find . -mtime +0 # find files modified greater than 24 hours ago
find . -mtime 0 # find files modified between now and 1 day ago
# (i.e., in the past 24 hours only)
find . -mtime -1 # find files modified less than 1 day ago (SAME AS -mtime 0)
find . -mtime 1 # find files modified between 24 and 48 hours ago
find . -mtime +1 # find files modified more than 48 hours ago
```

