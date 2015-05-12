# shells

## /etc/shells

The shells file contains a list of login shells on the system. Applications use this file to determine whether a shell is valid. For each shell a single line should be present, consisting of the shell's path, relative to the root of the directory structure (/).

        # cat /etc/shells

        #
        # /etc/shells
        #

        /bin/sh
        /bin/bash

        # End of file

## login incorrect

I added a user using this command

        useradd -m -G wheel -s /usr/bin/bash ving

The command seems ok, but when I tried to login as ving with the right password, it repeatedly said "login incorrect".

This is just because the shells file does not contain "/usr/bin/bash" although /usr/bin/bash is linked to /bin/bash.

When a shell program is installed in linux, its corresponding path is added to the shells file. When bash is installed along with arch linux it writes "/bin/bash" in the shells file. But after that arch linux’s installation linked /bin to /usr/bin. So whenever I enter "which bash" it returns "/usr/bin/bash". I used this path to add a user but it is not in the shells file.
