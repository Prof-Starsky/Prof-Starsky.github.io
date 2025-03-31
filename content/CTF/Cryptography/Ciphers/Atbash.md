# Tools:
https://www.dcode.fr/atbash-cipher




Very simple cipher, it just reverses the order of the alphabet so to say.

So:

| A   | B   | C   | D   | E   | F   | G   | H   | I   | J   | K   | L   | M   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Z   | Y   | X   | W   | V   | U   | T   | S   | R   | Q   | P   | O   | N   |
|     |     |     |     |     |     |     |     |     |     |     |     |     |
| N   | O   | P   | Q   | R   | S   | T   | U   | V   | W   | X   | Y   | Z   |
| M   | L   | K   | J   | I   | H   | G   | F   | E   | D   | C   | B   | A   |

So to encrypt 'Man'

M - N
a - Z
n - M

So 'Man' = 'NZM'

Note: Atbash doesn't notice casing, all letters are treated as capitals