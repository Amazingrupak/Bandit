# Bandit 2
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

Then I used the command ls and it showed the files in the directory

```
bandit0@bandit:~$ ls 
spaces in this filename
```
As the file has spaces in its name, it can't be dirrectly used as the command would consider each of them to be separate attribute.
So instead I'll put apostrophes to make it a single string
```
bandit2@bandit:~$ cat "spaces in this filename"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```
Or we can also use \ to say the next character will be a special character
```
bandit2@bandit:~$ cat spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```