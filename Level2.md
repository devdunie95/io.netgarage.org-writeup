##  Level 2	  -  ssh level2@io.netgarage.org

![8](https://user-images.githubusercontent.com/41302499/75866185-ad753b00-5e2a-11ea-8831-44a2c35702be.png)

####  Opening the `level02.c` file you can see:

	The number of args must be 2, (argv[0] being the caller's name).

	The two arguments should be numbers

	The catcher function will be called on the event `SIGFPE` (launched for example for a division by 0)

	The return value of the function is `argv[1]/argv[2]`

If the catcher function is called, it will set the current user identity, and print a win message, before spawning a new shell. 

This is clearly the indication that you  need to raise a `SIGFPE exception`.

![9](https://user-images.githubusercontent.com/41302499/75866187-ae0dd180-5e2a-11ea-9779-85b371f005cd.png)

What you can do instead is try to use an integer value outside of the bound of the integer definition. You can see on the `abs reference page` that the most-negative value to be out of range is -2147483648, because this will convert to 2147483648, above the MAX_INT value.

Level 3 password: `OlhCmdZKbuzqngfz`..

![10](https://user-images.githubusercontent.com/41302499/75866190-aea66800-5e2a-11ea-8ce6-25bc3ab809c4.png)
