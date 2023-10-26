#  Bandit 1
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
Using the password NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL I logged in and started the level.

Then I used the command ls and it showed the files in the directory

```
bandit0@bandit:~$ ls 
-
```
Now just cat - will not work as '-' is a symbol for an attribute
So instead I'll use ./ before the file name. This tells the command the directory of the file as well and the problem with it being a directory name doesn't happen.
```
bandit1@bandit:~$ cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```
Instead we could also use the angular bracket.
```
bandit1@bandit:~$ cat < -
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```
