[[Forensics]]
## Description

```
Frequencies-of-Deception
Forensics
Worth 822 Points
Easy
By Trent
```

An intercepted audio transmission carries a veiled warning. Some say it’s just noise, others believe it’s the key to an unsolved mystery. Use your forensic skills to dissect the frequencies and uncover the message lurking in the static. Flag format jctf{}

Note: For this challenge the flag format is NOT jctfv{} but is instead jctf{}

Then it had an attached 'unknown.wav' file

![[unknown (2).wav]]


## Solution

After listening to the wav file, I immediately recognized it as those old dial tones where each tone corresponded to a certain number/symbol (I can't believe this is considered old now). So I knew that I somehow had to decipher what tones corresponded with which numbers/symbols and had to collect them somehow.

I asked my teammates if they knew any program that could decipher this and Wxrth led me to a dtmf-detector, that led me to a nice app https://dtmf.netlify.app/

With that, I put in my unknown.wav file and left the sensitivity as 0.050 and got a nice output of

```
**Decoded:** 048049049048048049048048032048049048048049049049049032048049049048049049049048032048049048049048049048048032048049048049049049049049032048049048048048048049049032048048049049048048048048032048049049048049049048049032048049049048048049048049032048049048049049049049049032048048049048048049048048032048049049049048049048048032048049048048048048048049032048049048049049048048049032048049048049049049049049032048049049048048048048049032048049048049048049049049032048049048048048048048048032048049048049049048048049032048049048049049049049049032048049048048048049049048032048049049049048048049048032048048049049048048048048032048049048048049049048049032048049048049049049049049032048049049049048049048048032048049049048049048048048032048048049048048048048049032048049049049048048049049032048049048049049049049049032048049048049048048048048032048049049048049049048048032048049048048048048048048032048049049048048048049049032048049048048048049048049
```

I recognized that output as ASCII code so I then put it into an ASCII decoder and got:

```
01100100 01001111 01101110 01010100 01011111 01000011 00110000 01101101 01100101 01011111 00100100 01110100 01000001 01011001 01011111 01100001 01010111 01000000 01011001 01011111 01000110 01110010 00110000 01001101 01011111 01110100 01101000 00100001 01110011 01011111 01010000 01101100 01000000 01100011 01000101
```

Which I recognized as binary code, so I put that into Binary to text decoder and got:
dOnT_C0me_$tAY_aW@Y_Fr0M_th!s_Pl@cE


## Flag

I then wrapped that with the specific flag format for Frequencies-of-Deception and got the correct flag:
jctf{dOnT_C0me_$tAY_aW@Y_Fr0M_th!s_Pl@cE}

