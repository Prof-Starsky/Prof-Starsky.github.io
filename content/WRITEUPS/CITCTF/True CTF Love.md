[[Forensics]]
## Description
```
True CTF love
Forensics
Worth 552 Points
By boom
```

I got this strange email from another CTF participant not too long ago. I am just not sure what they mean by this...

Do you love CTFs as much as they do?

**SHA256:** `07cb654ce87444f158a52228848eb4eb501738913dfca44a2f227fb73ee9ed4b`

Then attached is a The_Flag_Well_Capture_Together.eml file.

## Solution

After opening the eml file as a txt file you get:
```
Return-Path: <ilovectfs19@waifu.club>
Delivered-To: idespisectfs14@memeware.net
Received: by mx1.mailhub.li (Postfix, from userid 65534)
	id 531FD380054; Tue, 22 Apr 2025 16:29:02 +0000 (UTC)
X-Spam-Checker-Version: SpamAssassin 3.4.2 (2018-09-13) on 4e7ad924bcc3
X-Spam-Level: 
X-Spam-Status: No, score=-1.3 required=5.0 tests=ALL_TRUSTED,BAYES_00,
	DKIM_SIGNED,DKIM_VALID,DKIM_VALID_AU,URIBL_BLOCKED,URIBL_SBL_A,
	URIBL_WS_SURBL shortcircuit=_SCTYPE_ autolearn=disabled version=3.4.2
Received: from mail.mailhub.li (unknown [10.69.4.14])
	by mx1.mailhub.li (Postfix) with ESMTPS id 98762380048
	for <idespisectfs14@memeware.net>; Tue, 22 Apr 2025 16:29:00 +0000 (UTC)
Authentication-Results: mx1.mailhub.li;
	dkim=pass (2048-bit key; unprotected) header.d=waifu.club header.i=@waifu.club header.b="e65uxTcZ";
	dkim-atps=neutral
MIME-Version: 1.0
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/simple; d=waifu.club; s=mail;
	t=1745339340; bh=HSq3Fk4UngoT3615kRTwX9TQfq9o0GNk3L5esFLg2e4=;
	h=Date:From:To:Subject:From;
	b=e65uxTcZ2s8RKde5x7GoMWDhM27qMUa2vpmCC6uPR/kCsC5Tl1lgVNCik9TBiIn7xThMSG0m17ElJR+eQ3IFACqhDjoJkCdLo+iYAwvx4Go1OOYUYRx7dn7tUisIKy2p7NsDjJMauF8H1fwIpO6kFZKUPiPescPp6mBJIWBOARUNxRSSReBJv+B8GibZJbN4c64c0 wOVpmrc1P3sGs/K1i8sjzcHVJyNdBBV2e71n5gJFfbo5EkM/HSmba8Vvfdg2BGkVaYOriRs9vs5+XwV8v9stPhL48avJipOSz1ykfbXW3//QZYpAOGyQz8lhE2cek5YLJulB yO/Pz8vtbkwjA==
	b=V293LCB3aGF0IGEgYmVhdXRpZnVsIGxpdHRsZSBwb2VtLiBJIGFsbW9zdCBzaGVkIGEgdGVhciByZWFkaW5nIHRoYXQuIEhvcGVmdWxseSB5b3UgbGVhcm5lZCBtb3JlIGFib3V0IGVtYWlsIGhlYWRlcnMuIEJ1dCBzZXJpb3VzbHksIGl0IGdldHMgbWUgd29uZGVyaW5nLi4uIGRvIHlvdSBsb3ZlIENURnMgYXMgbXVjaCBhcyB0aGV5IGRvPwoKQ0lUe2lfbDB2M19jdGYkX3QwMH0=
	
Content-Type: text/plain; charset=UTF-8;
 format=flowed
Content-Transfer-Encoding: 8bit
Date: Tue, 22 Apr 2025 12:29:00 -0400
From: ilovectfs19@waifu.club
To: idespisectfs14@memeware.net
Subject: =?UTF-8?Q?The_Flag_We=E2=80=99ll_Capture_Together?=
User-Agent: Roundcube Webmail/1.4.15
Message-ID: <94db41ae58ad070173fc571e2008de8b@waifu.club>
X-Sender: ilovectfs19@waifu.club

My dearest one, whose heart I hold,
In your eyes, I see a world untold.
Where logic and riddles dance like stars,
But you, my love, stand behind bars.

I know you don’t share in my joy,
The flags I chase, the games I deploy.
You sigh, you frown, and often retreat,
While I dive into challenges, so sweet.

But, oh, my love, can you see?
These puzzles are not just code to me.
They’re like whispers from a distant shore,
A challenge to unlock, a path to explore.

I dream of the day when you’ll join the chase,
And feel the thrill of solving with grace.
Not because you have to, but because you’ll find,
The joy in puzzles that ignites your mind.

I won’t push, I won’t rush,
No, I’ll be gentle, soft as a hush.
But if you ever wish to see what I see,
I’ll be here, waiting, with a flag for you and me.

Together, we can solve what’s unknown,
In the world of CTFs, you won’t be alone.
Let’s take it slow, no need to fear,
For love is the answer, my darling, my dear.

So, when you're ready, just take my hand,
Let’s solve the puzzle, make our stand.
And who knows, perhaps you’ll see—
That even CTFs, too, can be love’s key.
```

A lot of this is garbage and can completely be ignored, but there are some interesting lines, specifically in the DKIM header.

Usually in a DKIM header, there's only one signature (The 'b=') but take a look at the eml file and we have two signatures which is suspicious.

Looking at the signatures they both look like base64.
The first one when decoded gives:
```{®nÅ7ÚÏ)×¹Ç±¨1`á3nê1F¶¾™‚«Gù°.S—Y`TÐ¢“ÔÁˆ‰ûÅ8LHm&×±%%žCr�*¡:	'K£è˜ñàj58æa{v~íR++-©ìÛŒ“¸_Õü¤î¤’”>#Þ±Ãéê`I!`N
Å’EàI¿à|&Ù%³xs®Ó•¦jÜÔýìÏÊÖ/,7TœtUÙîõŸ˜	öèäIüt¦m¯½÷`Ø¤U¦®$löû9ù|òÿløKãÆ¯&*NK=r‘ö×[ÿA–)�á²C?%„MœzNX,›¥#¿??/µ¹0Œ```
which is complete gibberish, but by decrypting:
`V293LCB3aGF0IGEgYmVhdXRpZnVsIGxpdHRsZSBwb2VtLiBJIGFsbW9zdCBzaGVkIGEgdGVhciByZWFkaW5nIHRoYXQuIEhvcGVmdWxseSB5b3UgbGVhcm5lZCBtb3JlIGFib3V0IGVtYWlsIGhlYWRlcnMuIEJ1dCBzZXJpb3VzbHksIGl0IGdldHMgbWUgd29uZGVyaW5nLi4uIGRvIHlvdSBsb3ZlIENURnMgYXMgbXVjaCBhcyB0aGV5IGRvPwoKQ0lUe2lfbDB2M19jdGYkX3QwMH0=`
You get something interesting.
## Flag

After decryption you get:
```
Wow, what a beautiful little poem. I almost shed a tear reading that. Hopefully you learned more about email headers. But seriously, it gets me wondering... do you love CTFs as much as they do?
CIT{i_l0v3_ctf$_t00}
```
Which includes at the end the correct flag:
CIT{i_l0v3_ctf$_t00}