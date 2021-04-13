# mov eax, dword ptr some\_variable

In both cases you ask the processor to move the value from a specified address. It's one level of indirection. In the first case you ask it to take the address from a specified register. In the second case you specify an offset directly.

x86 processors don't support dual level indirection, so it's not possible to request to load a value from an address specified somewhere in memory - you have to load the address onto a register.

Under a number of assemblers \(MASM and built into VC++ assembler for example\) you could as well write just

```text
mov eax, dword ptr some_variable
```

without brackets, it would mean the same.

You could write

```text
mov eax, dword ptr [variable][ebx]
```

this would instruct to take the address of "variable", then add value of ebx and use the sum as an address from which to load a value. This is often used for accessing array elements by index. \(Variations on the syntax are supported, like `mov eax, dword ptr variable[ebx]` being commonly used and `mov eax, dword ptr [variable + ebx]` also being common.\)

In all these cases the processor would do the same - load a value from a specified address. It's one level of indirection each time.

[https://stackoverflow.com/questions/688799/dword-ptr-usage-confusion](https://stackoverflow.com/questions/688799/dword-ptr-usage-confusion)

