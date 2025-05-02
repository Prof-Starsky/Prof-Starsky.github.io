[[Forensics]]
## Description
```
Brainrot Quiz!
Forensics
Worth 480 Points
By boom
```

Bombardiro Crocodillo or....? You find out...

**SHA256:** `e5f5d4e97506233266904e460fdfea4fc3ce2bf1542dc122283835c545fb8516`

Then there's an attached pcap file
![[Pasted image 20250430133020.png]]

## Solution

After looking through each of the Echo (ping) requests and replies only 1 stands out as odd, number 11.
In number eleven it shows:
![[Pasted image 20250430141012.png]]
And in the hexadecimal/ASCII you'll find Q0lUe3RyNGw0bDNyMF90cjRsNGw0fQ== which looks exactly like base64 code.
## Flag

And decrypting Q0lUe3RyNGw0bDNyMF90cjRsNGw0fQ== through base64 gives the correct flag:
CIT{tr4l4l3r0_tr4l4l4}

