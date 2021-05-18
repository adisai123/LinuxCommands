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
