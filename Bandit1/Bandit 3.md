# Bandit3
I sshed into their server into port 2220 using :-
```
ssh bandit1@bandit.labs.overthewire.org -p 2220.
```
This opened the remote bandit terminal on my terminal and displayed the following text.
```
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit1@bandit.labs.overthewire.org's password:
```
Using the password rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi I logged in and started the level.

Then I used the command ls and it showed the files in the directory. There is the inhere directory. I cd into that directory.

```
bandit0@bandit:~$ ls 
inhere
bandit3@bandit:~$ cd inhere
```
Then I use ls but there's nothing in that folder.
```
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$
```
 I know that using the attribute -a shows all the files in a folder, even the hidden ones.
 ```
 bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
bandit3@bandit:~/inhere$ cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
 ```
