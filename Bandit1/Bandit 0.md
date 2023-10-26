# Bandit 0
First I sshed into their server into port 2220 using :-
```
ssh bandit0@bandit.labs.overthewire.org -p 2220.
```
This opened the remote bandit terminal on my terminal and displayed the following text.
```
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit0@bandit.labs.overthewire.org's password:
```
Using the password bandit0 I logged in and started the level.

Then I used the command ls and it showed the files in the directory

```
bandit0@bandit:~$ ls
readme
```
Using the command file I realised that it is a ascii text file and used the command cat to read it.
```
bandit0@bandit:~$ file readme
readme: ASCII text
bandit0@bandit:~$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```
That is the password for the next level