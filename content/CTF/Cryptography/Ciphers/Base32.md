#Base
# Tools:
https://www.dcode.fr/base-32-encoding
https://gchq.github.io/CyberChef/
https://cryptii.com/pipes/base32 especially good for the different variants of Base32


Base32 is a binary to text encoding scheme that represents binary data in an ASCII string format


Uses:
![[Pasted image 20250212091006.png]]
Or it uses:
![[Pasted image 20250212091334.png]]
Or it uses:
![[Pasted image 20250212092007.png]]
Or it uses:
![[Pasted image 20250212092042.png]]
Note they also have '=' as an index 32 of sorts
= Is a padding character that doesn't change the meaning

The most common alphabet is RFC 4648



Example:

Take the source string "Man"

In ASCII:

M-77
a-97
n-110

That ASCII in bits then equals:

77 - 01001101
97 - 01100001
110 - 01101110

Putting those strings together you get

010011010110000101101110


Then separating those into sets of 5 bits:

01001 - 9
10101 - 21
10000 - 16
10110 - 22
1110 - NAN
but instead of giving an error, you add ones until you get full set, then append an = at the end:
11100 - 28
 - =
Then putting that from ASCII into the Base32 alphabet

9 - J
21 - V
16 - Q
22 - W
28 - 4
= - =

So the encrypted text would be:
'Man' = JVQW4= 



