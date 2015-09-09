# bandit 16

    # ssh bandit16@bandit.labs.overthewire.org
    password: cluFn7wTiGryunymYOu4RcffSxQluehd

    # nmap -p 31000-32000 localhost
    PORT      STATE SERVICE
    31046/tcp open  unknown
    31518/tcp open  unknown
    31691/tcp open  unknown
    31790/tcp open  unknown
    31960/tcp open  unknown

    # nmap -sV -p 31046,31518,31691,31790,31960 localhost
    PORT      STATE SERVICE VERSION
    31046/tcp open  echo
    31518/tcp open  msdtc   Microsoft Distributed Transaction Coordinator (error)
    31691/tcp open  echo
    31790/tcp open  msdtc   Microsoft Distributed Transaction Coordinator (error)
    31960/tcp open  echo

    # echo cluFn7wTiGryunymYOu4RcffSxQluehd | openssl s_client -quiet -connect localhost:31791

It returns a private key and save the private key in file /tmp/ving/rsa.

    # chmod 400 rsa
    # ssh -i rsa bandit17@localhost
    # cat /etc/bandit_pass/bandit17
    xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn

