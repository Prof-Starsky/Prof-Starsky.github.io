[[Cryptography]] [[RSA Cipher]]

## Description

```
The-Hidden-Key
Cryptography
Worth 100 points
Easy
By Dylan
```

An anonymous party was using Wireshark looking network activity and stumbled across this encrypted text, they then notified NICC and sent the file. This could be a key to something.

Then it had a link download to a 'TheHiddenKey.txt' file which contained:

```
n: 20167919
e: 65537
ct: [10254726, 8086048, 6236280, 17208595, 10736836, 5882601, 15516508, 7658876, 2682380, 10736836, 15449006, 6236280, 11933731, 5504792, 922598, 11933731, 758869, 5504792, 17208595, 4826125, 7658876, 5504792, 2682380, 4744868, 12442849, 4826125, 7658876, 1039218, 15449006, 6236280, 2682380, 4826125, 4744868, 4111665]
```


## Solution

Immediately after seeing the txt file I recognized it as an RSA cipher because of the recognizable Public Key Value, e, and Ciphertext.

So, in order to solve the RSA you have to follow the following steps for each ciphertext:
- Factorize n to find p and q
- Compute ϕ(n)=(p−1)(q−1)
- Find d as the modular inverse of e modulo ϕ(n)
- Compute m = c^d mod(n)
- Use m and the ASCII alphabet to find what letter each ciphertext corresponds to

I then wrote a simple program that ran through the above steps for each of the ciphertexts

```
from sympy import isprime, gcdex

from math import isqrt

  

def factorize_n(n):

    for i in range(2, isqrt(n) + 1):

        if n % i == 0:

            p, q = i, n // i

            if isprime(p) and isprime(q):

                return p, q

    return None, None

  

def modinv(e, phi):

    d, _, _ = gcdex(e, phi)

    return d % phi

  

def rsa_decrypt(n, e, ct):

    p, q = factorize_n(n)

    if not p or not q:

        raise ValueError("Failed to factorize n")

    phi = (p - 1) * (q - 1)

    d = int(modinv(e, phi))

  

    decrypted = [pow(c, d, n) for c in ct]

    return ''.join(chr(m) for m in decrypted)

  

# Given values

n = 20167919

e = 65537

ct = [10254726, 8086048, 6236280, 17208595, 10736836, 5882601,

      15516508, 7658876, 2682380, 10736836, 15449006, 6236280, 11933731,

      5504792, 922598, 11933731, 758869, 5504792, 17208595, 4826125,

      7658876, 5504792, 2682380, 4744868, 12442849, 4826125, 7658876,

      1039218, 15449006, 6236280, 2682380, 4826125, 4744868, 4111665]

  

# Decrypt and print the message

try:

    decrypted_message = rsa_decrypt(n, e, ct)

    print("Decrypted message:", decrypted_message)

except ValueError as err:

    print("Error:", err)
```


## Flag 

After running the above code, it output the correct flag:
jctfv{Pr1v@t3_k3y_f0r_1nF0rm@t10n}