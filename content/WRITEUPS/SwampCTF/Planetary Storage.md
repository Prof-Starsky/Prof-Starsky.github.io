[[Forensics]]

## Description

```
Planetary Storage
Forensics
Worth 200 Points
```


My friend found this strange file while perusing his computer, but we can't read it. Can you figure out what it is and get the information from it?

Difficulty: Easy/Medium

The flag is in the standard format

It also had a download link to a 'PlanetaryStorage.zip' file which contained:
![[Pasted image 20250331210431.png]]

## Solution

After searching through each file, I found that CURRENT, CURRENT.bak, LOCK, MANIFEST-000012 contained nothing of interest; LOG contained a little bit of data on the .ldb files, but not much of interest still; while the .ldb files contained a lot of information.

Starting in 000002.ldb, I found a base64 string called the payload:

```
"payload":"eyJrZXkiOiJcIjdiZjFjNTRlLTA5MjAtNGU2Zi1iNTBiLTE0ZDgzODY3NDdmN1wiIiwib3AiOiJQVVQiLCJ2YWx1ZSI6ImV5SmtZWFJoSWpwYklsUm9hWE1pTENKcGN5SXNJbUVpTENKeVpXUWlMQ0pvWlhKeWFXNW5JU0pkTENKcFpDSTZJbHdpTjJKbU1XTTFOR1V0TURreU1DMDBaVFptTFdJMU1HSXRNVFJrT0RNNE5qYzBOMlkzWENJaWZRPT0ifQ=="
```

which when decrypted gave another base64 string:

```
{"key":"\"7bf1c54e-0920-4e6f-b50b-14d8386747f7\"","op":"PUT","value":"eyJkYXRhIjpbIlRoaXMiLCJpcyIsImEiLCJyZWQiLCJoZXJyaW5nISJdLCJpZCI6IlwiN2JmMWM1NGUtMDkyMC00ZTZmLWI1MGItMTRkODM4Njc0N2Y3XCIifQ=="}
```

And when you decrypt that you get:

```
{"data":["This","is","a","red","herring!"],"id":"\"7bf1c54e-0920-4e6f-b50b-14d8386747f7\""}
```

So I went on and starting digging into the 000007.ldb file and found another base64 string called the payload:

```
eyJrZXkiOiJcIjNhNDdiYmZiLTgyMmMtNDU1Mi04N2VjLTUyNTA4ZDk0OGJkOFwiIiwib3AiOiJQVVQiLCJ2YWx1ZSI6ImV5SmtZWFJoSWpwYklsUm9hWE1pTENKcGN5SXNJbUVpTENKeVpXUWlMQ0pvWlhKeWFXNW5JU0pkTENKcFpDSTZJbHdpTTJFME4ySmlabUl0T0RJeVl5MDBOVFV5TFRnM1pXTXROVEkxTURoa09UUTRZbVE0WENJaWZRPT0ifQ==
```

which gave another base64 string, which when decrypted gave:

```
{"data":["This","is","a","red","herring!"],"id":"\"3a47bbfb-822c-4552-87ec-52508d948bd8\""}
```

So I went on and started digging into the 000010.lbd file hoping that there wasn't just another red herring. Then I yet another base64 string called the payload:

```
eyJrZXkiOiJcIjMzNTc5M2Q1LTRhYzEtNDgyMy05MmM3LWZkM2I1YTZhMmEwN1wiIiwib3AiOiJQVVQiLCJ2YWx1ZSI6ImV5SmtZWFJoSWpwYkluTjNZVzF3UTFSR2V6RndaalV0WWpRMU0yUXRaRFEzTkdJME5UTjlJbDBzSW1sa0lqb2lYQ0l6TXpVM09UTmtOUzAwWVdNeExUUTRNak10T1RKak55MW1aRE5pTldFMllUSmhNRGRjSWlKOSJ9
```

which gave another base64 string when decrypted:

```
{"key":"\"335793d5-4ac1-4823-92c7-fd3b5a6a2a07\"","op":"PUT","value":"eyJkYXRhIjpbInN3YW1wQ1RGezFwZjUtYjQ1M2QtZDQ3NGI0NTN9Il0sImlkIjoiXCIzMzU3OTNkNS00YWMxLTQ4MjMtOTJjNy1mZDNiNWE2YTJhMDdcIiJ9"}
```

And when I decrypted that I got:

```
{"data":["swampCTF{1pf5-b453d-d474b453}"],"id":"\"335793d5-4ac1-4823-92c7-fd3b5a6a2a07\""}
```

which finally wasn't a red herring
## Flag

So using the only non-red herring, I got the correct flag:
