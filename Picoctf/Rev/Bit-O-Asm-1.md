# Bit-O-Asm-1
The problem statement
```
Can you figure out what is in the eax register? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}. Download the assembly dump here.
```
The file downloaded is an ascii text file with assembly in it.
```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x4],edi
<+11>:    mov    QWORD PTR [rbp-0x10],rsi
<+15>:    mov    eax,0x30
<+20>:    pop    rbp
<+21>:    ret
```
<+15>:    mov    eax,0x30. This line moves the the hexadecimal number to the register called eax. And that is the value in that register. The number in decimal is 48. Therefore the flag is picoCTF{48}. :D