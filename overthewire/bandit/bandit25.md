# bandit 25

    # ssh bandit25@bandit.labs.overthewire.org
    password: uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

    # cat /etc/passwd | grep bandit26
    bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext

    # cat /usr/bin/showtext

    #!/bin/sh

    more ~/text.txt
    exit 0

The text.txt is only 6 lines.
Make my terminal's heigth less than 6 lines to get a page break.

    # ssh -i bandit26.sshkey bandit26@localhost

Enter "v" to start up a editor(vi).
Then type ":r /etc/bandit_pass/bandit26" and the password will be shown.

    5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z

