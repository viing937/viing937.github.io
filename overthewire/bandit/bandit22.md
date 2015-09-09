# bandit 22

    # ssh bandit22@bandit.labs.overthewire.org
    password: Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

    # cat /usr/bin/cronjob_bandit23.sh

    myname=$(whoami)
    mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
    echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
    cat /etc/bandit_pass/$myname > /tmp/$mytarget

    # cat /tmp/8ca319486bfbbc3663ea0fbe81326349
    jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

