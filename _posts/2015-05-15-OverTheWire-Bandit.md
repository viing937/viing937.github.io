---
title: OverTheWire Bandit Level 0-25
layout: post
---

* TOC
{:toc}

More information is available [here](http://overthewire.org/wargames/bandit/).

# 1. Level 0

```
$ ssh bandit0@bandit.labs.overthewire.org
password: bandit0
```

```
$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

# 2. Level 1

```
$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

# 3. Level 2

```
$ cat spaces\ in\ this\ filename
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

# 4. Level 3

```
$ cat inhere/.hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

# 5. Level 4

```
$ file inhere/*
inhere/-file00: data
inhere/-file01: data
inhere/-file02: data
inhere/-file03: data
inhere/-file04: data
inhere/-file05: data
inhere/-file06: data
inhere/-file07: ASCII text
inhere/-file08: data
inhere/-file09: data
```

```
$ cat inhere/-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

# 6. Level 5

```
$ find inhere/ -size 1033c -exec cat {} \;
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

# 7. Level 6

```
$ find / -size 33c -user bandit7 -group bandit6 -exec cat {} \;
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

# 8. Level 7

```
$ grep millionth data.txt
millionth       cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

# 9. Level 8

```
$ cat data.txt | sort | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

# 10. Level 9

```
$ cat data.txt | grep -a '==='
truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

# 11. Level 10

```
$ cat data.txt | base64 --decode
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

# 12. Level 11

```
$ cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

# 13. Level 12

```
$ mkdir /tmp/ving
$ cp data.txt /tmp/ving
$ cd /tmp/ving
$ xxd -r data.txt > data
```

Then extract the compressed file repeatedly using gunzip and bunzip2.

```
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

# 14. Level 13

```
$ ssh -i sshkey.private bandit14@localhost
```

```
$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

# 15. Level 14

```
$ echo 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e | nc localhost 30000
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

# 16. Level 15

```
$ echo BfMYroe26WYalil77FoDi9qh59eK5xNr | openssl s_client -quiet -connect localhost:30001
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
```

# 17. Level 16

```
$ nmap -p 31000-32000 localhost
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown
```

```
$ nmap -sV -p 31046,31518,31691,31790,31960 localhost
PORT      STATE SERVICE VERSION
31046/tcp open  echo
31518/tcp open  msdtc   Microsoft Distributed Transaction Coordinator (error)
31691/tcp open  echo
31790/tcp open  msdtc   Microsoft Distributed Transaction Coordinator (error)
31960/tcp open  echo
```

```
$ echo cluFn7wTiGryunymYOu4RcffSxQluehd | openssl s_client -quiet -connect localhost:31790
```

It returns a private key and save the private key in file `/tmp/ving/rsa`.

```
$ chmod 400 rsa
$ ssh -i rsa bandit17@localhost
```

```
$ cat /etc/bandit_pass/bandit17
xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
```

# 18. Level 17

```
$ diff passwords.new passwords.old
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> BS8bqB1kqkinKJjuxL6k072Qq9NRwQpR
```

# 19. Level 18

```
$ scp bandit18@bandit.labs.overthewire.org:~/readme ./
```

```
$ cat readme
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

# 20. Level 19

```
$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

# 21. Level 20

```
$ echo GbKksEFF4yrVs6il55v6gwY5aVje5f0j | nc localhost -l 7999
```

Then open another shell via ssh.

```
$ ./suconnect 7999
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```

The password for the next level will be shown in the first shell.

```
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

# 22. Level 21

```
$ cat /etc/cron.d/cronjob_bandit22
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

```
$ cat /usr/bin/cronjob_bandit22.sh
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

```
$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

# 23. Level 22

```
$ cat /usr/bin/cronjob_bandit23.sh
```

```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

```
$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

# 24. Level 23

Create a shell script `/var/spool/bandit24/shell.sh`.

```bash
#!/bin/bash

mkdir /tmp/ving
cat /etc/bandit_pass/bandit24 > /tmp/ving/pass
```

```
$ chmod 777 /var/spool/bandit24/shell.sh
```

```
$ cat /tmp/ving/pass
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

# 25. Level 24

Create a shell script `/tmp/ving/shell.sh`

```bash
#!/bin/bash

i=1000
while [ $i -lt 10000 ]
do
    echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i | nc localhost 30002 > /tmp/ving/log.txt
    i=$(($i+1))
done
```

```
$ bash /tmp/ving/shell.sh
```

```
$ cat /tmp/ving/log.txt | sort | uniq
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```

# 26. Level 25

```
$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

```
$ cat /usr/bin/showtext
```

```bash
#!/bin/sh

more ~/text.txt
exit 0
```

The text.txt is only 6 lines. Make terminal's heigth less than 6 lines to get a page break.

```
$ ssh -i bandit26.sshkey bandit26@localhost
```

Enter `v` to start up a editor(vi). Type `:r /etc/bandit_pass/bandit26` and the password will be shown.

```
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
```
