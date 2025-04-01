[[Miscellaneous]]

## Description

```
Lost in Translation
Misc
Worth 158 points
```


We found this program which we know has a flag somewhere, but nothing we've tried has been able to extract it. Can you figure it out?

To run the program, you can use NodeJS (recommended version 18.17.1 or higher).


It also had a download link to a 'Translate.zip' file which contained:

![[Pasted image 20250331214515.png]]



## Solution

After reading through each of these files, one of my teammates yoshixi noticed that the challenge.js file had some whitespace code hidden through the file.

So, using https://www.dcode.fr/whitespace-language , I inputted the entire challenge.js file into it in order to decrypt the whitespace code.

## Flag

That decryption output the correct flag:
swampCTF{Whit30ut_W0rk5_W0nd3r5}