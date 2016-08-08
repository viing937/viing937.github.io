# Bandit

## level 0

```
$ ssh bandit0@bandit.labs.overthewire.org
password: bandit0
```

```
$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

## level 1

```
$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

## level 2

```
$ cat spaces\ in\ this\ filename
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

## level 3

```
$ cat inhere/.hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

## level 4

```
$ file inhere/*
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
```

```
$ cat inhere/-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

## level 5

```
$ find inhere/ -size 1033c -exec cat {} \;
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

## level 6

```
$ find / -size 33c -user bandit7 -group bandit6 -exec cat {} \;
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

## level 7

```
$ grep millionth data.txt
millionth       cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

## level 8

```
$ cat data.txt | sort | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

## level 9

```
$ cat data.txt | grep -a '==='
truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```
