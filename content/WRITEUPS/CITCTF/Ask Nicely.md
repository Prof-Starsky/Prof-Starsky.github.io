[[Forensics]]
## Description
```
Ask Nicely
Forensics
Worth 668 Points
By ronnie
```

I made this program, you just have to ask really nicely for the flag!

And attached is a file 'asknicely'.
## Solution

When you run asknicely it asks:
`example% ./asknicely`
`How badly do you want the flag?`
No matter how you respond it then says:
`Ask nicely...`
Then if you respond incorrectly it says:
`that's not quite what I'm lookng for.`

So it's clear that we need to find the right input/phrase that it's looking for.

So I then disassembled the code and got the following:
![[Pasted image 20250430130831.png]]
![[Pasted image 20250430130909.png]]
![[Pasted image 20250430130936.png]]

After looking through it, I noticed that after it tells me to 'Ask nicely...' it will either output "Good job, I'm so proud of you!" or "that's not quite what I'm looking for".
And in the aGoodJobIMSoPro side you can also see:
`call    _Z9give_flagNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEE ; give_flag(std::string)`
So it's safe to assume that by getting the aGoodJobIMSoPro option it will output the flag

But we still need to find out the right input.

So if you look through fastcall main, you'll notice a line that stands out:
`lea     rdx, aPrettyPrettyPr ; "pretty pretty pretty pretty pretty plea"...`
which seems like the Ask Nicely phrase we're looking for
So if you dig a little deeper you get:
`.rodata:0000000000576030 aPrettyPrettyPr db 'pretty pretty pretty pretty pretty please with sprinkles and a ch'`
which is close but not complete, so if you use shift+f12 in IDA to view the strings you'll find:
![[Pasted image 20250430132155.png]]
which seems like the right phrase, 'pretty pretty pretty pretty pretty please with sprinkles and a cherry on top'.

## Flag

So if you run the asknicely program with the right inputs:
`example% ./asknicely
`How badly do you want the flag?
`This input doesn't matter
`Ask nicely...
`pretty pretty pretty pretty pretty please with sprinkles and a cherry on top

It outputs:
`Good job, I'm so proud of you!
And it outputs the correct flag: CIT{2G20kX09yF3F}



