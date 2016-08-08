# Bandit

## level 10

```
$ cat data.txt | base64 --decode
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

## level 11

```
$ cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

## level 12

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

## level 13

```
$ ssh -i sshkey.private bandit14@localhost
```

```
$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

## level 14

```
$ echo 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e | nc localhost 30000
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

## level 15

```
$ echo BfMYroe26WYalil77FoDi9qh59eK5xNr | openssl s_client -quiet -connect localhost:30001
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
```

## level 16

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

It returns a private key and save the private key in file ```/tmp/ving/rsa```.

```
$ chmod 400 rsa
$ ssh -i rsa bandit17@localhost
```

```
$ cat /etc/bandit_pass/bandit17
xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
```

## level 17

```
$ diff passwords.new passwords.old
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> BS8bqB1kqkinKJjuxL6k072Qq9NRwQpR
```

## level 18

```
$ scp bandit18@bandit.labs.overthewire.org:~/readme ./
```

```
$ cat readme
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

## level 19

```
$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```
