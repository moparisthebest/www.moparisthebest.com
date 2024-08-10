+++
title = "Against Silos+Signal"
date = 2024-08-08
category = "xmpp"
author = "moparisthebest"
+++

Recently a self-proclaimed "security researcher" published a blog [post](https://soatok.blog/2024/08/04/against-xmppomemo/) where they entirely miss the point and make the worst recommendation possible, to use Signal.  Here's the short and simple reason you should ignore it.

<!-- more -->

The point that seems to go right over their heads is:

<span style="font-size:1.5em; font-style: italic;">It doesn't actually matter how cryptographically secure your end-to-end encryption is when 1 entity controls all ends, and can instantly update them whenever they want.</span>

This is what Signal and all other silos get you.  That's it.  That's all you need to read, you can close the tab now.  But I will continue to expand on this a bit more below if you wish to continue...

If you are unfamiliar with the term, a silo is a centralized system "that functions apart from others especially in a way seen as hindering communication and cooperation". In the context of internet platforms, a silo is the opposite of an open, federated system.  Silos exists to lock users in instead of giving them freedom.  Prominent examples are Signal, WhatsApp, AOL Instant Messenger, Facebook, Twitter etc etc.

The post goes on to explain how XMPP is not a competitor to Signal.  I agree, it's not even close.  [XMPP](https://xmpp.org/) is an open, federated, standardized protocol, which means it serves *you*, the user.  You can choose your own server: both software and host, or host it yourself.  You can choose your own clients, use many at the same time from many platforms.  If XMPP doesn't do something you need, it's eXtensible, you can do this yourself without permission from anyone, or propose a standard which others can implement too.  You can use XMPP with your own domain name forever, no one can turn it off on you.  You don't need a phone number to use it.

If you like your client with e2e and the author does something stupid, like [create a shitcoin and force it on you](https://www.wired.com/story/signal-mobilecoin-cryptocurrency-payments/), or [force you to set an insecure 4 digit PIN and upload all your data to themselves](https://blog.cryptographyengineering.com/2020/07/10/a-few-thoughts-about-signals-secure-value-recovery/), you can just switch clients.  They don't control the server so they can't [ban you from using another client](https://github.com/LibreSignal/LibreSignal/issues/37#issuecomment-217211165).  And your contacts don't need to know or care because your address never changes.

*Nothing* is a competitor to XMPP.  Signal and most other silos don't want to be, because they are in it for the user lock-in, and the VC money they hope might come from it one day.  When it doesn't, they *will* sell your data or shut it down.  XMPP has been around for over 25 years while dozens of silos have came and gone, it will be around in another 25 years, Signal will not.  Stop the endless silo hopping, hop to XMPP and never leave.  If you are capable of running your own server for your family and friends I suggest [Snikket](https://snikket.org/start/), if you just want a good server hosted by someone else, [Conversations.im](https://account.conversations.im/).

Because people have brought it up, I want to stress that while forming a [Threat Model](https://blog.jmp.chat/b/2022-privacy-threat-modelling) is critical before considering privacy, it is not applicable in any way to my main point up above.  This is because there is no threat model where you need sound e2e to protect you from a provider, but trust that same provider to push any code they want to your system silently and automatically.  That simply doesn't make sense.

Lastly, just because people might ask if any of the "findings" are legitimate, yes, one: The version of the BouncyCastle library used by Conversations needed to be updated, [it already has been](https://codeberg.org/iNPUTmice/Conversations/commit/f764b24ffc1089cad147887053d8b64d8207b248), a real security researcher would have let the dev know, instead of publishing a sensational blog post with a silly conclusion.

Here are some links if you would like more in depth reading on the subject:  
  * [OMEMO Author Tim Henkes' response to the blog, which was moderated](https://www.moparisthebest.com/tim-henkes-omemo-response.txt)
  * [https://snikket.org/blog/products-vs-protocols/](https://snikket.org/blog/products-vs-protocols/)
  * [https://blog.jabberhead.tk/2019/12/29/re-the-ecosystem-is-moving/](https://blog.jabberhead.tk/2019/12/29/re-the-ecosystem-is-moving/)
  * [https://gultsch.de/objection.html](https://gultsch.de/objection.html)

Use XMPP, stay free!
