# test

The TEST instruction performs an implied AND operation between corresponding bits in the two operands and sets the flags without modifying either operand. 

 The format for the TEST instruction is: 

`TEST reg, reg` 

`TEST reg, mem` 

`TEST reg, immed` 

`TEST mem, reg` 

`TEST mem, immed` 

reg, mem, and immed can be 8, 16, or 32 bits.



The [`test eax, eax`](https://en.wikipedia.org/wiki/TEST_%28x86_instruction%29) is the same as `and eax, eax` \(bitwise `and`\) _except_ that it doesn't store the result in `eax`. So `eax` isn't affected by the test, but the zero-flag is, for example.

The `test eax, eax` is necessary to make the `jne` work in the first place. And `jne` is the same as `jnz`, just as `je` is the same as `jz`. Both act based on the ZF \(zero-flag\) value.

The `jne` branch will be taken _if_ ZF=0 and therefore whenever `strcmp` returns a non-zero value \(i.e. strings not equal\). Conversely if `eax` contains zero upon return from `strcmp`, the jump via `jne` will _not_ happen.



