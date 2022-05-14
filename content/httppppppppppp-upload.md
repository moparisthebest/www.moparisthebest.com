+++
title = "httppppppppppp-upload: full drive exploit"
date = 2022-05-14
category = "XMPP"
author = "moparisthebest"
+++

The discovery and mitigation of httppppppppppp-upload and code to exploit it.

<!-- more -->

For background, downloading files shared via [http upload](https://xmpp.org/extensions/xep-0363.html) in XMPP is generally a 2 step process:

1. HEAD request to determine size of file (returned in `Content-Length:` header)
2. If user clicks download, or if under some set size, GET request to download the file

Problem #1
----------

So sometime in late March 2022 it struck me that an evil HTTP server could lie in the HEAD request, and serve an unlimited sized file in the GET request.  A few minutes of writing code later and I had [evil-http](https://github.com/moparisthebest/evil-http).  The initial mode responded that the file was 11kb and actually served a file of configurable length (0 means unlimited), I deployed it to my server with a limit of 100mb, and using gajim's XML console sent an HTTP Upload link to it, Conversations said "download 11kb file?", I clicked it, and it downloaded the entire 100mb... oops.  Dino did the same.  Gajim had a ? for the size, but downloaded the whole file with no way to cancel it.  This means if I turned on the unlimited mode and shared a file in any MUC, I could entirely fill up the hard drives of all victims who clicked download, and they wouldn't even have a way to stop it.  I immediately contacted the Conversations, Dino, and Snikket devs (Daniel, larma, MattJ respectively) to explain the problem.

Additionally I realized I could configure nginx to gzip compress my unlimited-size-response so many 0s could be returned using minimal bandwidth.

At some point MattJ commented that he'd wondered what would happen in the event of ridiculous headers...

Problem #2
----------

What if [evil-http](https://github.com/moparisthebest/evil-http) returned an unlimited number of headers? Turns out: bad things.  A few minutes of work and I had a mode that returned unlimited randomly named headers.  If a naive HTTP client kept them in a Map or something it would run out of memory.  Turns out Conversations' HTTP client aborted after a few KB, but Dino's is irrevocably broken and can't be worked around without upgrading to the latest version, which is blocked by something else, fun!

Solution(s)
-----------

1. Conversations has a [handful](https://github.com/iNPUTmice/Conversations/commit/7e762eb799abe0d4f172d04eb714b97e838a8b1f) [of](https://github.com/iNPUTmice/Conversations/commit/eadb1e127b81005b8d83a86197e6c71ce0115fcc) [commits](https://github.com/iNPUTmice/Conversations/commit/95e3a6769d6cdc08ff86d70fb8cb561974346501) to:  
    a. request uncompressed file size  
    b. only download up to that size
2. Dino [allows file transfers to be cancelled](https://github.com/dino/dino/commit/193bf38a790b2a124493c3b7ad591f826e0f773d)
3. Gajim [allows file tranfers to be cancelled](https://dev.gajim.org/gajim/gajim/-/commit/57924ca86061d60634bfa3ff0253b9d481f0f906)
4. Siskin [only downloads the number of bytes returned in HEAD request](https://github.com/tigase/siskin-im/commit/2a9adecbbdccee880e1d587d65ed2d2be899ccca)

(Impossibility of) Coordinated Disclosure
-----------------------------------------

With such a widespread bug, it was impossible to coordinate releases or anything like that.  I told the devs I knew personally, at least one of them told devs they knew personally (after asking), and when those were fixed, I made an announcement in [jdev](xmpp:jdev@muc.xmpp.org?join) that client devs who implement HTTP upload should contact me via XMPP or email.  Over the next week or so, I got *many* emails from devs asking for details (as an aside I was surprised they didn't contact me via XMPP), who I explained the bug to, and *most* of them were vulnerable.  Hopefully by now they are all fixed, I haven't seen this exploited in the wild in public MUCs, and I'm in most of them so I assume the script kiddies aren't paying attention. :)

Advice for HTTP-using devs
--------------------------

1. You have no guarantee headers will end, limit these to something sane, maybe 16k of headers or something
2. You have no guarantee data returned by the HEAD request will match that returned by the GET request.
3. Beware transer-chunked encoding.
4. Always have a way to cancel or a sane limit.

For XMPP client devs specifically, this advice applies to downloading HTTP Uploaded files, POSH files, host-meta files, and anything else you might grab over HTTP.  Honestly just beware [any stream that may be unlimited](https://www.moparisthebest.com/eatxmempp-cve-2021-32918/).

For questions/comments, please comment on the fediverse post [here](https://moparisthe.best/notice/AJQsVZls0TKjh3ke7E)
