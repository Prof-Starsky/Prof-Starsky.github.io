[[Reverse Engineering]]
## Description
```
Read Only
Reverse Engineering
Worth 534 Points
By ronnie
```

Here we go!

Flag Format: CIT{example_flag}

Then attached is a file 'readonly'

## Solution

Since the file is called readonly, I suspected that I would find the flag somewhere inside the code, and not by running it.
So when I disassemble the code I get:
![[Pasted image 20250501122449.png]]
Then I decided to click into each of the programs

## Flag

And by clicking into sub_407C05
![[Pasted image 20250501122635.png]]
We get the correct flag:
CIT{87z1BjG1968G}