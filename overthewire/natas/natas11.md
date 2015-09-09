# [natas 11](http://natas11.natas.labs.overthewire.org)

    Username: natas11
    Password: U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK

We get the cookie and we konw what the cookie means, so run the code below.

    #include <stdio.h>

    int main()
    {
        int i;
        char data[] = "{\"showpassword\":\"no\",\"bgcolor\":\"#ffffff\"}";
        char encrypt[] = "\x0a\x55\x4b\x22\x1e\x00\x48\x2b\x02\x04\x4f\x25\x03\x13\x1a\x70\x53\x19\x57\x68\x5d\x55\x5a\x2d\x12\x18\x54\x25\x03\x55\x02\x68\x52\x11\x5e\x2c\x17\x11\x5e\x68\x0c";
        for ( i = 0; i < sizeof(data) && i<sizeof(encrypt); i++ )
            printf("%c", data[i]^encrypt[i]);
        printf("\n");
        return 0;
    }

The result show the key of xor encrypting.

    qw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jqw8Jq

Get the cookie which we need with the key "qw8J".

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

Replace old cookie with the new.

    ClVLIh4ASCsCBE8lAxMacFMOXTlTWxooFhRXJh4FGnBTVF4sFxFeLFMK

Refresh the page.

    The password for natas12 is EDXp0pS26wLKHZy1rDBPUZk0RKfLGIR3

