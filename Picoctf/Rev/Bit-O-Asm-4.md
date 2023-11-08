# Bit-O-Asm-4
The problem statement:
```
Can you figure out what is in the eax register? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}. Download the assembly dump here.
```
The assembly code is
```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret
```
The jle stands for jump is less than or equal to and the jmp stands for just jump. The lines jump to the line mentioned. The jle line only jumps if the comparison satisfies the condition. 0x9fe1a(654874) is moved to the address "DWORD PTR [rbp-0x4]" and it is compared with 0x2710(10000). 0x9fe1a is obviously greater, so jle command is ignored and 0x65(101) is subtracted from it. Then it jumps to line <main+41> and eax takes the value in "DWORD PTR [rbp-0x4]". Eax has the value 654773 and the flag is picoCTF{654773}. :D