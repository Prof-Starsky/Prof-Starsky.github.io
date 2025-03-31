[[Forensics]]

## Description
```
evtx
Forensics
Worth 453 Points
Easy
By Jan
```

It appears that one of the low-level grunts of the NICC organization have gone rogue. They keep trying to get into a user's account by guessing their password. Can you tell us 1. the name of the user who is being targeted with brute force password guessing attempts and 2. the number of times the rogue user has tried to get into the account? The flag should have the format jctfv{Name_Number} where Name is the username and Number is the count.

It then had a download to a 'evtx.zip' which contained a Windows XML EventLog file 'chal.evtx'

In that file, it contained 141 different events
![[Pasted image 20250331155954.png]]


## Solution
After looking through every event, I found that all events with Event ID 4625 corresponded to a failed log on which is what I need for the flag.

So, there 17 different instances of failed logons, but they weren't necessarily brute force failed attempts, they could've been a regular user just mis-entering their password, so I had to dig a little deeper.

![[Pasted image 20250331160903.png]]

After inspecting each of the failed attempts, I was able to see that odds are, the brute force attempts went from
1:28:16 to 1:29:04

So I inspected each of the attempts between 1:28:16 and 1:29:04 and each of them looked very similar to:

![[Pasted image 20250331161201.png]]

and were all targeted at User500, whereas any of the failed login attempts after 1:29:04 looked similar to: 

![[Pasted image 20250331161254.png]]
![[Pasted image 20250331161313.png]]

and were targeted at random users, which made me think these were just accidental failed-logons

So, I counted each of the failed logon attempts on User500 between 1:28:16 and 1:29:04 and found there were 11 attempts.

## Flag
I then took User500 and 11, and put it into the flag format for this questions: jctfv{Name_Number} and got the correct flag:
jctfv{User500_11}


