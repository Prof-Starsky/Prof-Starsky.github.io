#Base
# Tools:
https://www.base64decode.org/
https://www.dcode.fr/base-64-encoding
https://gchq.github.io/CyberChef/


Base64 is a binary to text encoding scheme that represents binary data in an ASCII string format

Uses:
![[Pasted image 20250211100755.png]]
There are two versions that have a different 62/63rd character
![[Pasted image 20250212092158.png]]
Note the standard Base64 also has '=' as an index 64 of sorts
= Is a padding character that doesn't change the meaning


# Example:

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

Then, by separating that into sets of 6 bits you get
010011 - 19
010110 - 22
000101 - 5
101110 - 46

In the table above. in Base64 those translate to:
19 - T
22 - W
5 - F
46 - u


So, 'Man' using Base64 translates to 'TWFu'


If for example, you only had 'Ma'
In ASCII, it would be
M-77
a-91

in binary:
77 - 01001101
91 - 01100001

In sets of 6 bits:

010011 - 19
010110 - 22
0001 -NAN

But instead of raising an error, it then appends 0's til you have a set of 6 bits, and appends an '=' at the end of the string

so 0001 becomes
000100 - 4

And:
19 - T
22 - W
4 - E
Appended =

So 'Ma' translates into 'TWE='





An example of a challenge where this is useful is:

[[ISSESSIONS CTF]] Easy Key 4

You've intercepted a base64 password and its right here : YWhJc2VleW91Z290X3RoZXBhc3N3b3JkLXlvdS13aW4. Yogur task is to unlock the true fla. In puzzles like this, balance is key. Maybe this string equals the flag if something is added. But you must be careful since too many cooks spoil the broth. You must change the recipe without changing the taste. Can this even be done? It may be possible to change the password without changing the meaning.

You also got this weird one. I don't know what they are. It could be helpful since it looks like base64.

CoCwpgBAZgNghgcwgSwM4QC7gE5gDQQCeA9gK4QhwBukyGmOYAdC00A==

rZjetu8D7gfy4QnZAJGRMGwb5tBLUBcvUvkY3LEK2dxjVzNE6kT1ou09Un1mEVqN5jR===

=

YruDaoDF4AWD5MbtsDi=====


The solution to this was to take YWhJc2VleW91Z290X3RoZXBhc3N3b3JkLXlvdS13aW4 and add =====
So the final key was bhbureauCTF{YWhJc2VleW91Z290X3RoZXBhc3N3b3JkLXlvdS13aW4 ===== } as adding the '=' doesn't change the decoded text at all.
