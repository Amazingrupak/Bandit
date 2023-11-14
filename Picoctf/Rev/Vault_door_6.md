# Vault door 6
The problem statement:
```
This vault uses an XOR encryption scheme. The source code for this vault is here: VaultDoor6.java
```
The code given in the question is:
```
import java.util.*;

class VaultDoor6 {
    public static void main(String args[]) {
        VaultDoor6 vaultDoor = new VaultDoor6();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Dr. Evil gave me a book called Applied Cryptography by Bruce Schneier,
    // and I learned this really cool encryption system. This will be the
    // strongest vault door in Dr. Evil's entire evil volcano compound for sure!
    // Well, I didn't exactly read the *whole* book, but I'm sure there's
    // nothing important in the last 750 pages.
    //
    // -Minion #3091
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            0x3b, 0x65, 0x21, 0xa , 0x38, 0x0 , 0x36, 0x1d,
            0xa , 0x3d, 0x61, 0x27, 0x11, 0x66, 0x27, 0xa ,
            0x21, 0x1d, 0x61, 0x3b, 0xa , 0x2d, 0x65, 0x27,
            0xa , 0x66, 0x36, 0x30, 0x67, 0x6c, 0x64, 0x6c,
        };
        for (int i=0; i<32; i++) {
            if (((passBytes[i] ^ 0x55) - myBytes[i]) != 0) {
                return false;
            }
        }
        return true;
    }
}

```

As we can see the bytes of the password is being xored with 0x55 and then subtracted by the bytes in mybytes, one by one. So we can just xor the input bytes with 0x55 and we will ge the bytes in the password. Doing that I get the password in ascii. Here's the output and the code.
```
x = [ 0x3b, 0x65, 0x21, 0xa , 0x38, 0x0 , 0x36, 0x1d, 0xa , 0x3d, 0x61, 0x27, 0x11, 0x66, 0x27, 0xa ,0x21, 0x1d, 0x61, 0x3b, 0xa , 0x2d, 0x65, 0x27,0xa , 0x66, 0x36, 0x30, 0x67, 0x6c, 0x64, 0x6c]
for i in x:
    y = i^0x55
    print(y)
```
```
110 48 116 95 109 85 99 72 95 104 52 114 68 51 114 95 116 72 52 110 95 120 48 114 95 51 99 101 50 57 49 57
```
Here's the flag: 
```
picoCTF{n0t_mUcH_h4rD3r_tH4n_x0r_3ce2919}
```