[[Steganography]]
## Description
```
Blank Image
Steganography
Worth 589 Points
By ronnie
```

I was gonna make a really cool challenge but then I literally forgot about it so all I have is this blank image. Good luck!

And attached is a completely blank image:
![[Pasted image 20250430122252.png]]

## Solution

By putting the blank image into Aperisolve.com you're able to use it's ZSteg function and you're able to find that of the 8x17 pixels some of them have alpha = 0 or alpha = 1 in the alpha channel. Taking those and interpreting it as binary gives
`01000011 01001001 01010100 01111011 01101110 00110001 01000110 00110000 01010010 01110011 01101101 00110000 01000101 01110010 00110100 00110000 01111101`


## Flag

When you decrypt the binary into text you get the correct flag:
CIT{n1F0Rsm0Er40}
