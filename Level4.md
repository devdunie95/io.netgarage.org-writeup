###  Level 4	ssh level4@io.netgarage.org

![19](https://user-images.githubusercontent.com/41302499/75866216-b49c4900-5e2a-11ea-956a-af82cc9f30b0.png)

The code for this one is straightforward and only call a system command with the `popen` function, reads its input and display it.

Under a shell, the binaries are found by searching the `PATH` variable until one executable file with the desired name is found.

In the code, it is susceptible to an attack that changes the `$PATH` environment variable because it is not using an absolute path to call `whoami`.

The OS will look at `$PATH` for list of directories to search the binary for in a left to right order. When it finds a binary that has the requested name, it will execute that binary.

You can trick the OS into running our own `whoami` program that spawn a shell. As long as our directory comes before the actual location of `whoami`, your binary will be run instead.

You can make a directory for yourselves to put the above C source code.

Next, compile the program with the same name as `whoami`.

You have prepended a "." in the `$PATH`. The OS will start searching from current directory first for a `whoami`. You can see that your equid is level5.

![20](https://user-images.githubusercontent.com/41302499/75866218-b534df80-5e2a-11ea-8e39-34ba79bb2b15.png)

Level 5 password: 
