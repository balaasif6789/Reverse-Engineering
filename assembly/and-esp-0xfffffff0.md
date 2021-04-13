# and-esp-0xfffffff0

 `and esp,0xfffffff0` enforces 16 byte stack alignment, which is a common ABI requirement. It does this by masking out \(setting to zero\) the least significant 4 bits of the stack pointer, which is equivalent to rounding down to the nearest multiple of 16.

It creates a so called stack frame and aligns it to addresses which can be divided by 16:

1. Save stackframe pointer from calling programm in stack: `push ebp`.
2. Create new stackframe pointer for the program which is called: `mov ebp, esp`
3. Align stack to addresses which can be divided by 16 by setting the lowest 4 bit to 0: `and esp, -16`
4. Create 16 byte space in stack for example for local variables and stuff: `sub esp, 0x10`

**Why align?**  
The cpu always reads 16 bytes of data at once \(depends on cpu type\). But it reads only from an address which can be divided by 16: 0x0, 0x10, 0x20,.... And so on, because the lowest 4 bit are not used in the address bus. They are "missing". When you read more than a byte from an address, the cpu may have to read twice, because your address is directing to a dword or sth like that, that is right at the end of one address which can be divided by 16 and your dword reaches already into the next address divideable by 16. By aligining the stack to addresses which are divideable by 16, you reduce the risk of that happening, when working with the stack.

You can see that in the sample you posted. The value of ESP is on the left and aligned to addresses divideable by 16. Easy to see because of the ending `0`:

```text
0xbffffb70: 
0xbffffb80: 
0xbffffb90: 
0xbffffba0: 
0xbffffbb0: 
0xbffffbc0: 
0xbffffbd0: 
0xbffffbe0:
```

