#Hashing 
[[MD5]]
[[BCrypt]]
[[SHA1]]
[[SHA256]]
[[SHA512]]
[[Blowfish]]



Idea for solving hashes where it goes

This is the encrypted text, it has been encrypted 20 times by 'a' 50 times by 'b' then 100 times by 'c' with a known list of words for what the original is.
Instead of try to directly decrypt, go through each word in the known list and hash them forward and compare to the encrypted text, if it matches that's the word
(Highest use case is with rock_you)