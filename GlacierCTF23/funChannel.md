# Category:
pwn

# Challenge:
Fun Channel

# Description:
"Good luck getting my secret password hehe. (Note: There are a lot of files in the current directory. The flag file has an arbitrary name, is the only file that ends with .txt and consists only of numbers 0-9 and letters. a-zA-Z)". Flag format is still gctf{.*}

author: Xer0
nc chall.glacierctf.com 13383

# Solve:
The challenge lets us use 3 syscalls only: read, getdents and openat. Additionally the shellcode cant extend the length of 0x7c Bytes.
To solve the challenge we need to:
* leak the filename
* read filename and leak flag.

```
# leaks filename using side channel attack (timeouts)
exploit_1.py

# leaks file content using the same method as first exploit
exploit_2.py
```
* Note: the was one an Issue with leaking 1 specific byte at index 10 (always returned 0), so i had to bruteforce that.

* FLAG: gctf{W41t_d1D_yoU_R3aLlY_r3Bu1Ld_L$?}
