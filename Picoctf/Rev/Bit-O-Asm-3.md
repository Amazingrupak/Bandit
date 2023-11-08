# Bit-O-Asm-3
The problem statement:
```
Can you figure out what is in the eax register? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}. Download the assembly dump here.
```
Downlooding the file we are greeted with some assembly code again.
```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret
```
We can see "DWORD PTR [rbp-0xc]" is pointing to 0x9fe1a and "DWORD PTR [rbp-0x8]" is pointing to 0x4. Eax is taking the value at "DWORD PTR [rbp-0xc]" and is multiplied by the value at "DWORD PTR [rbp-0x8]". Then 0x1f5 is added to eax. and then it is just moved to an address and moved back to eax. The final value after all the operations is 2619997. Hence the flag is picoCTF{2619997}. :D