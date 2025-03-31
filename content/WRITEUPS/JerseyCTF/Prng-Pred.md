[[Cryptography]] [[XOR Cipher]]
## Description

```
Prng-Pred
Cryptography
Worth 919 Points
Hard
By KDShetty11
```

We created a custom random number generator using XOR-Shift to help us generate pseudorandom numbers. THere may have been an issue with our initialization. Here are the first 5 generated values. Can you predict the next one?
[http://prng-pred.aws.jerseyctf.com:5000/](http://prng-pred.aws.jerseyctf.com:5000/)

The link led to a website that looked like this:
![[Pasted image 20250331145110.png]]




## Solution

The problem provided five sequential outputs from an XOR-Shift based pseudorandom number generator (PRNG) with the goal to determine the next number in the sequence. I realized that because XOR-Shift generators are deterministic, we could infer the shift parameters used in the PRNG, so we could predict the next number

That led to me developing the following program:
Using the given sequence '2796150728, 1619295863, 4160883531, 3273899421, 3467984294' I brute-force all reasonable values for the shift parameters a, b, c

(Note the generated sequence is different every time you load the page, so you have to edit the progam accordingly)

```
def xorshift(x, a, b, c):

    # Perform the XOR-shift steps with given shift parameters.

    # All operations are done on 32-bit unsigned integers.

    x ^= (x << a) & 0xFFFFFFFF

    x ^= (x >> b)

    x ^= (x << c) & 0xFFFFFFFF

    return x & 0xFFFFFFFF

  

# Given sequence

sequence = [2796150728, 1619295863, 4160883531, 3273899421, 3467984294]

  

# We'll search for shift parameters a, b, c in a reasonable range (e.g. 1 to 31)

valid_parameters = []

  

for a in range(1, 32):

    for b in range(1, 32):

        for c in range(1, 32):

            valid = True

            x = sequence[0]

            # Test if the recurrence holds for the entire provided sequence.

            for expected in sequence[1:]:

                x = xorshift(x, a, b, c)

                if x != expected:

                    valid = False

                    break

            if valid:

                # Compute the next value using these parameters.

                next_val = xorshift(sequence[-1], a, b, c)

                valid_parameters.append(((a, b, c), next_val))

  

if valid_parameters:

    print("Found valid shift parameters and their predicted next values:")

    for params, next_val in valid_parameters:

        print(f"Shift parameters a, b, c = {params} --> Next value = {next_val}")

else:

    print("No valid shift parameters found in the tested range.")
```

After running the script, it output:
```
Found valid shift parameters and their predicted next values:
Shift parameters a, b, c = (13, 7, 17) --> Next value = 2506751581

```

## Flag
After inputting 2506751581 into the website it confirmed that my prediction was right and outputted the flag:
jctfv{Predictable_PRNG_Rizzed}