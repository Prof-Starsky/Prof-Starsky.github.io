[[Steganography]]
## Description
```
I AM Steve
Steganography
Worth 644 Points
By kristine
```

You were supposed to be a hero, Brian!

**SHA256:** `01b3dbe5d8801adf27a9bb779d85ef4c8881905544642fbdbdd41e54e4d0ae5e`

Then it had the following image attached:
![[ChickenJockey (1).png]]
## Solution

By putting the chicked_jockey image into Aperisolve you're able to use its Zsteg function to find the hidden text VEhJU19pc19hX2NyYWZ0aW5nX3RhYmxl which looks exactly like base64 encrypted text.-

## Flag

And after decrypting VEhJU19pc19hX2NyYWZ0aW5nX3RhYmxl through base64 and wrapping it with CIT{} you get the correct flag:
CIT{THIS_is_a_crafting_table}
