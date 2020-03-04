###  Level 3	ssh level3@io.netgarage.org

The level 3 starts the same way the level2 does.

![11](https://user-images.githubusercontent.com/41302499/75866192-af3efe80-5e2a-11ea-9b35-92a1312293a0.png)

looking at the source code.

  1.	good is the function to call to clear the stage

  2.	bad seems to be the default function, referenced in the main.

  3.	The only argument need to be string of length more than 4

  4.	All chars of the argument will be copied in the buffer (max of 50)

  5.	All chars except last 4 ones will be set to 0

The 4. part actually duplicate the value of argv[2] into buffer.

![12](https://user-images.githubusercontent.com/41302499/75866196-afd79500-5e2a-11ea-95e8-ff6de6dcc791.png)

This program introduce the concept of bufferoverflow to overwrite nearby local variable (more specifically, variables below the buffer).

![13](https://user-images.githubusercontent.com/41302499/75866197-b0702b80-5e2a-11ea-850d-80af2be01c9b.png)

`gdb peda` is a GDB plugin that helps greatly in visualization of registers, instructions and stack content. This is a great tool for dynamic analysis.

![14](https://user-images.githubusercontent.com/41302499/75866200-b108c200-5e2a-11ea-9087-837acc2dea40.png)

When you `disass main`, it can be very scary to see a long list of assembly code. When you are experienced enough, you can figure out which offset refers to which variable. 

I will assume you are beginners hence one of way I usually do is to look out for functions that reference those local variables.

![15](https://user-images.githubusercontent.com/41302499/75866201-b1a15880-5e2a-11ea-8d45-c6be449b9128.png)

From the source code, we know that `printf` will have a string as argument1 and `functionpointer `as argument2.

The calling convention of x86 for function is to have argument on the top of stack. Then argument 2 below argument 1...

`gdb-peda$ x/s 0x80486c0
0x80486c0:	"This is exciting we're going to %p\n"`

With `gdb` examine, you can confirm that argument1 really contain the string.

So `functionpointer` is located at esp+0x4. However, I would recommend you find a reference that uses `ebp` instead of esp. This is because the value of `ebp` is constant in a stack frame whereas `esp` can vary.

   `0x0804856d <+165>:	mov    eax,DWORD PTR [ebp-0xc]
   0x08048570 <+168>:	call   eax`

This is another place that reference your `functionpointer`. Notice call `eax` from this, you know function pointer is at `ebp-0xc`.
You can do the same to find out where is `buffer`.

Now, you just need to find the distance between buffer and `functionpointe`r.

Run python inside /levels and then get this value.

  `>>> 0x58-0xc
  76`

####  Testing out

![16](https://user-images.githubusercontent.com/41302499/75866203-b2d28580-5e2a-11ea-881b-57b114a92437.png)

![17](https://user-images.githubusercontent.com/41302499/75866208-b36b1c00-5e2a-11ea-89f1-40a1735c2921.png)

####  Exploit

Level 4 password: `7WhHa5HWMNRAYl9T`

![18](https://user-images.githubusercontent.com/41302499/75866213-b403b280-5e2a-11ea-9cd6-c54bb2770bce.png)
