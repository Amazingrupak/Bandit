# Two sum
The problem statement:
```
Can you solve this? What two positive numbers can make this possible: n1 > n1 + n2 OR n2 > n1 + n2 Enter them here nc saturn.picoctf.net 50548. Source
```
The question states a mathematically impossible problem, but it is possible if we think about how binary data works. The first bit is the sign. If it is 0, the number is positive and if it is 1, the number is negative.

A 4 bit number has 16 numbers. If it is unsigned, it goes upto 15. But if it is signed, it goes from -8 to 7. So for int, if we input 2147483647 2147483646, that will be 111111... . SO it does, accept that as an input but when we add, the number can be signed so the code think they are both negative as the first bit is 1. And the sum would be negative. 

Here's the source code:
```
#include <stdio.h>
#include <stdlib.h>

static int addIntOvf(int result, int a, int b) {
    result = a + b;
    if(a > 0 && b > 0 && result < 0)
        return -1;
    if(a < 0 && b < 0 && result > 0)
        return -1;
    return 0;
}

int main() {
    int num1, num2, sum;
    FILE *flag;
    char c;

    printf("n1 > n1 + n2 OR n2 > n1 + n2 \n");
    fflush(stdout);
    printf("What two positive numbers can make this possible: \n");
    fflush(stdout);
    
    if (scanf("%d", &num1) && scanf("%d", &num2)) {
        printf("You entered %d and %d\n", num1, num2);
        fflush(stdout);
        sum = num1 + num2;
        if (addIntOvf(sum, num1, num2) == 0) {
            printf("No overflow\n");
            fflush(stdout);
            exit(0);
        } else if (addIntOvf(sum, num1, num2) == -1) {
            printf("You have an integer overflow\n");
            fflush(stdout);
        }

        if (num1 > 0 || num2 > 0) {
            flag = fopen("flag.txt","r");
            if(flag == NULL){
                printf("flag not found: please run this on the server\n");
                fflush(stdout);
                exit(0);
            }
            char buf[60];
            fgets(buf, 59, flag);
            printf("YOUR FLAG IS: %s\n", buf);
            fflush(stdout);
            exit(0);
        }
    }
    return 0;
}

```
Here's the flag :D
```
$ nc saturn.picoctf.net 50548
n1 > n1 + n2 OR n2 > n1 + n2
What two positive numbers can make this possible:
2147483647
2147483646
You entered 2147483647 and 2147483646
You have an integer overflow
YOUR FLAG IS: picoCTF{Tw0_Sum_Integer_Bu773R_0v3rfl0w_f6ed8057}
```