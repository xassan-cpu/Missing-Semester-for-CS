## Lecture 1 Exercise Solutions


### 2. Create a new directory called `missing` under `/tmp`.

`mkdir /tmp/missing`

### 3. Look up the `touch` program. The `man` program is your friend.

`man touch`

### 4. Use `touch` to create a new file called `semester` in `missing`.


`cd /tmp/missing`

`touch semester`


### 5. Write the following into that file, one line at a time:
```
#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
```


`echo '!/bin/sh' > semester`

`echo "curl --head --silent https://missing.csail.mit.edu" >> semester`


### 6. Try to execute the file, i.e. type the path to the script (`./semester`) into your shell and press enter.Udnerstand why it doesn't work by consulting the output `ls` (hint: look at the permission bits of the file).

`./semester`

> `-bash: ./semester: Permission denied`

`ls -l`

> `-rw-r--r-- 1 amin amin 61 Oct  1 00:37 semester`

We (the owner) don't have permission to execute this file.

### 7. Run the command by explicitly starting the `sh` interpreter, and giving it to the file `semester` as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn't?

`sh semester`
>```
HTTP/2 200
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Thu, 08 Aug 2024 20:16:01 GMT
access-control-allow-origin: *
etag: "66b52781-205d"
expires: Tue, 01 Oct 2024 05:46:14 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: A391:56A91:450B006:4DF8248:66FB8A4D
accept-ranges: bytes
age: 0
date: Tue, 01 Oct 2024 06:44:28 GMT
via: 1.1 varnish
x-served-by: cache-yyc1430024-YYC
x-cache: HIT
x-cache-hits: 0
x-timer: S1727765068.476791,VS0,VE92
vary: Accept-Encoding
x-fastly-request-id: 083e492d5ce34bf326f4e232939548736de905f9
content-length: 8285


### 8. Look up the `chmod` program (e.g. use `man chmod`).


`man chmod`

>```
...
chmod [OPTION]... MODE[,MODE]... FILE...
...
The  format  of  a  symbolic mode is [ugoa...][[-+=][perms...]...], where perms is either zero or more letters
from the set rwxXst, or a single letter from the set ugo.  Multiple symbolic modes can be given, separated  by
commas.
...


### 9. Use `chmod` to make it possible to run the command `./semester` rather than having to type `sh semester`.


`chmod u+x semester`

`ls -l`

>`-rwxr--r-- 1 amin amin 61 Oct  1 00:37 semester`

We (the owner) have permission to execute `semester`.

`./semester`

>```
HTTP/2 200
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Thu, 08 Aug 2024 20:16:01 GMT
access-control-allow-origin: *
etag: "66b52781-205d"
expires: Tue, 01 Oct 2024 05:46:14 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: A391:56A91:450B006:4DF8248:66FB8A4D
accept-ranges: bytes
age: 0
date: Tue, 01 Oct 2024 06:54:32 GMT
via: 1.1 varnish
x-served-by: cache-yyc1430022-YYC
x-cache: HIT
x-cache-hits: 0
x-timer: S1727765672.050208,VS0,VE85
vary: Accept-Encoding
x-fastly-request-id: a711953e381684d4d795f117c4c1c90421766fe1
content-length: 8285


### 10. Use `|` and `>` to write the “last modified” date output by semester into a file called last-modified.txt in your home directory.

`./semester | head -n12 | tail -n1 > ~/last-modified.txt`

`cat ~/last-modified.txt`

>
>`date: Tue, 01 Oct 2024 06:54:32 GMT`

### 11. Write a command that reads out your laptop battery’s power level or your desktop machine’s CPU temperature from `/sys`. Note: if you’re a macOS user, your OS doesn’t have sysfs, so you can skip this exercise.'

`cd /sys/class/power_supply/BAT1`

`cat capacity`
>`100`


