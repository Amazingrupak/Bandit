# Bandit 5
Problem statement tells me that I need to find a file with the properties :-

1) Human readable

2) 1033 bytes 

3) non executable

I'll be using the command find with the attributes ! exectuable, readable and size
```
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
bandit5@bandit:~/inhere$ find ! -executable -size 1033c -readable
./maybehere07/.file2
```
Then I cat the file 
```
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```