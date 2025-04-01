[[Cryptography]] [[Hashing]]

## Description

```
Rock my Password
Cryptography
Worth 150 Points
```

I've come up with an extremely secure(tm) way to store my password, noone will be able to reverse it! I've hashed it with md5 100 times, then sha256 100 times, then sha512 100 times! There's no way you're going to be able to undo it >:3 I'll even tell you it was in the RockYou database, and the password is 10 characters long, that's how confident I am!

The flag is in the format: swampCTF{RockYouPassword}

As a reminder, please don't flood our infrastructure with guesses.

Hashed Password (Flag): f600d59a5cdd245a45297079299f2fcd811a8c5461d979f09b73d21b11fbb4f899389e588745c6a9af13749eebbdc2e72336cc57ccf90953e6f9096996a58dcc

Note: The entire flag (swampCTF{rockyoupassword}) was hashed to get the provided hash, not just rockyoupassword


## Solution

After first looking at this challenge, I tried to come up with some way to brute force the hashed password, but quickly realized that it would take a near infinite amount of time. 

So, one of my teammates Jacky came up with the idea to instead, hash every 10 character password in the RockYou database through md5 100 times, sha256 100 times, then sha512 100 times and compare it against the already hashed password. In his words 'cause hashing forward is really fast'.

So I implemented it just like that. I created a program that went through every 10 character password in the RockYou data base, hash it 300 times, and compare it to the target hash as shown below:

```
import hashlib

  

# Function to hash a given string 100 times with MD5, then SHA-256, then SHA-512

def custom_hash(password):

    hashed = password.encode()

  

    # MD5 x 100

    for _ in range(100):

        hashed = hashlib.md5(hashed).digest()

  

    # SHA-256 x 100

    for _ in range(100):

        hashed = hashlib.sha256(hashed).digest()

  

    # SHA-512 x 100

    for _ in range(100):

        hashed = hashlib.sha512(hashed).digest()

  

    return hashed.hex()

  

# Given hash to match

target_hash = "f600d59a5cdd245a45297079299f2fcd811a8c5461d979f09b73d21b11fbb4f899389e588745c6a9af13749eebbdc2e72336cc57ccf90953e6f9096996a58dcc"

  

# Path to RockYou wordlist (update if needed)

rockyou_path = "C:/Documents/SWAMPCTF/rockyou (1).txt"

  

# Read the RockYou file and process only 10-character passwords

with open(rockyou_path, "r", encoding="latin-1") as f:

    for password in f:

        password = password.strip()

        if len(password) == 10:  # Only check 10-character passwords

            formatted_password = f"swampCTF{{{password}}}"  # Wrap in flag format

            if custom_hash(formatted_password) == target_hash:

                print(f"FOUND FLAG: swampCTF{{{password}}}")

                break
```



## Flag

After running the above program, it output the correct flag:
swampCTF{secretcode}