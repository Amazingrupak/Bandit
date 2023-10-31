# File Types
This is the problem statement

```
This file was found among some files marked confidential but my pdf reader cannot read it, maybe yours can. You can download the file from here.
```
After downloading, I opened my terminal and ran the file command.
```
$ file Flag.pdf
Flag.pdf: shell archive text
```
the sh command will extract the data. It gives me a new file called flag. Running file command, It tells me that the file is a current ar archive.
I then used binwalk -e to extract that data.
```
$ file flag
flag: current ar archive
$ binwalk -e flag

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
100           0x64            bzip2 compressed data, block size = 900k
```
I find a directory called _flag.extracted. Going into the directory I find a file called 64. Running file command I find that it is a gzip file. I ran gzip -d and extracted that. It gave me a lzip file. I did the same procedure a couple of times. These are the commands I used.
```
$ cd _flag.extracted/
$ ls
64
$ file 64
64: gzip compressed data, was "flag", last modified: Thu Mar 16 01:40:17 2023, from Unix, original size modulo 2^32 327
$ mv 64 64.gz
$ gzip -d 64.gz
$ file 64
64: lzip compressed data, version: 1
$ mv 64 64.lz
$ lzip -d 64.lz
$ file 64
64: LZ4 compressed data (v1.4+)
$ mv 64 64.lz4
$ lz4 -d 64.lz4
Decoding file 64
64.lz4               : decoded 265 bytes
$ file 64
64: LZMA compressed data, non-streamed, size 254
$ mv 64 64.lzma
$ lzma -d 64.lzma
$ file 64
64: lzop compressed data - version 1.040, LZO1X-1, os: Unix
$ mv 64 64.lzo
$ lzop -d 64.lzo
$ file 64
64: lzip compressed data, version: 1
$ mv 64 64.lz
$ lzip -d 64.lz
$ file 64
64: XZ compressed data, checksum CRC64
$ mv 64 64.xz
$ xz -d 64.xz
$ file 64
64: ASCII text
$ cat 64
7069636f4354467b66316c656e406d335f6d406e3170756c407431306e5f
6630725f3062326375723137795f37396230316332367d0a
```
I decoded that in dcode.fr using the ascii coding and I got the flag.