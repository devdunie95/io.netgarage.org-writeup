###  Level 01
ssh level1@io.netgarage.org

Running level01 ask for a 3 digits number which we will find inside the binary.

![image001](https://user-images.githubusercontent.com/41302499/75864765-8584d800-5e28-11ea-87e0-23d0ccbd598e.png)

You can find a “Readme File”. Using vi command you can see the instruction of that file.

![2](https://user-images.githubusercontent.com/41302499/75866159-a9491d80-5e2a-11ea-907d-1ed7bdb0c66f.png)

You can see that there is no source code for level01. This means that we have to reverse engineer the logic to get to level2. 
From this simple file command, we can see that it is Executable Linkable Format. 32 bits architecture and written for the intel CPU.

![3](https://user-images.githubusercontent.com/41302499/75866164-a9e1b400-5e2a-11ea-844f-1b6d8d50923d.png)

Running the strings utility

![4](https://user-images.githubusercontent.com/41302499/75866170-ab12e100-5e2a-11ea-8f5f-01dcc30da289.png)

Launching the program under gdb:

![5](https://user-images.githubusercontent.com/41302499/75866174-abab7780-5e2a-11ea-9358-3b3738154c1d.png)

Show the disassembly code for the main function (entry point of the program)
The first call print the question with puts. The second one asks for the user input (the password. Then the program compares a fixed value with the value of the register eax.
This value is a hexadecimal value, you can display its decimal value with p in gdb:

![6](https://user-images.githubusercontent.com/41302499/75866179-ac440e00-5e2a-11ea-8438-25ba3f0b2cf3.png)

So apparently, we are comparing the entered value, which is stored in the eax register.
je will jump to the label if the values are equal, since this jump is to the YouWin section, we can assume the password is 271.
Then using cat /home/level2/.pass command, you can see the password for level 02.
The password for level2 is XNWFtWKWHhaaXoKI .

![7](https://user-images.githubusercontent.com/41302499/75866181-acdca480-5e2a-11ea-9acf-190efd4c844b.png)

