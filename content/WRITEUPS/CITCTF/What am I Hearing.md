[[Miscellaneous]]
## Description
```
What am I Hearing
Misc
Worth 941 Points
```

Bro what am I hearing rn

Flag Format: CIT{example_flag}

And attached is this wav file:
![[flag (1).wav]]

## Solution

After listening to the wav file, it's pretty obvious that it's morse code.
So I used https://morsefm.com/ in order to quickly decode it and I got:`....................!?.?...?.......?...............?....................?.?.?.?.!!?!.?.?.?!!!!!!!.............!.......................!..?..............................................!.!!!.?.!!!!!!!!!!!!!!!!!!!!!!!!!!!.!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!.........!..?!!!!!!!!!!!!!!!!!.?.!!!!!!!!!!!!!.........................................!.!!!!!!!!!.................................!.?.................................................!..?..........!..?!!!!!!!!!...............................!.`
Which at first seems like nothing, but it's too precise to be nothing as there weren't morse code translation errors they specifically were coded to . ! and ?
And when you have seemingly random periods, exclamation points, and question marks you can guess it's the stupid programming language only used to mess up people in CTFs: Ook!

## Flag

So, using https://www.dcode.fr/ook-language I input the decoded morse code and got the correct flag:
CIT{zG48r2FBR6Wn}