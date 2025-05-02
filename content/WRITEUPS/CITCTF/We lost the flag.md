[[Forensics]]
## Description
```
We lost the flag
Forensics
Worth 655 Points
By boom
```

Sorry everyone, we unfortunately lost the flag for this challenge.

**SHA256:** `d1058ed414e6e45f4d2c7cc41baf73b3778a80be18cdf2d6470348c72ab01dfd`

Then attached is a corrupted file lost.png

## Solution

When you initially try to open the png, it appears that it is corrupted/broken, so we have to take a closer look at it.

So, by using hexedit lost.png, we're able to see the problem with the image:
![[Pasted image 20250502123940.png]]
Instead of this being a png as it's named, it's actually a JPEG so trying to open it as a png definitely won't work, so we can simply rename the file to lost.jpg
But, now if we try to open it we'll get a error still that the file is corrupted. So, looking at the Hex again, or using jpeginfo in order to diagnose it, we find that this isn't a valid jpeg because it starts with 0x00 0xc2 whereas for a proper jpeg it's expected to start with FF D8

So using hexedit again in order to edit the first two values we get:
![[Pasted image 20250502124913.png]]
## Flag

Now when we try to open lost.jpg we get
![[Pasted image 20250502125048.png]]
Which contains the correct flag:
CIT{us1ng_m4g1c_1t_s33m5}
