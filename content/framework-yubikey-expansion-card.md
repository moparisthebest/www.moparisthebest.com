+++
title = "Frame.work YubiKey Expansion Card"
date = 2024-04-05
category = "hacks"
author = "moparisthebest"
+++

How I built a [YubiKey](https://www.yubico.com/) [Expansion Card](https://github.com/FrameworkComputer/ExpansionCards) for the [frame.work](https://frame.work/) laptop.

<!-- more -->

I use a YubiKey as a [PGP Card](https://drduh.github.io/YubiKey-Guide/) but the biggest downside is how much it sticks out, so I can't leave it in, and so can easily forget it.  They do make a [Nano](https://www.yubico.com/us/product/yubikey-5-series/yubikey-5-nano/) that would be *mostly* hidden, but not entirely, and that's $60 I might not need to spend. I wanted a nice integrated YubiKey, and my new ryzen frame.work 13 had these nice modules where one could maybe fit.  I searched and found [some prior art](https://community.frame.work/t/yubikey-5c-adapter/23157) but it didn't look that great and still stuck out some.  So I built one:

[![module](/pics/framework-yubi/module.jpg)](/pics/framework-yubi/module.jpg)
[![installed](/pics/framework-yubi/installed.jpg)](/pics/framework-yubi/installed.jpg)

The YubiKey touch sensor can be easily triggered by touching the silver wire.  So now the how... I took apart one of my USB-C expansion cards to see how much room was in there, turns out, plenty.  I had an extra YubiKey and [pictures of a teardown of an older version](https://www.hexview.com/~scl/neo5/) gave me confidence nothing important was in the back (looks like only NFC antennas to me). So, after measuring how long the YubiKey would have to be to fit in the expansion card shell, I put a high-speed cut-off wheel in the dremel and chopped the back of the YubiKey off.  I booted an old laptop to plug the card in to see if it still worked (didn't want to risk burning out my frame.work :)), it did!

[![cut-in-half](/pics/framework-yubi/cut-in-half.jpg)](/pics/framework-yubi/cut-in-half.jpg)

I put some electrical tape over the cut end since there are some exposed traces there, and did a test fit in the module, problem #1 was that the USB-C plug didn't come out *quite far enough* to stay firmly plugged in, comparing to the USB-C module, it was maybe 1/8th inch too short.  So, using my knife, I scored around it and pushed hard on each side and it kind of cracked off perfectly.  The black around the YubiKey looks like plastic but it's more like ceramic.

[![plug-trim](/pics/framework-yubi/plug-trim.jpg)](/pics/framework-yubi/plug-trim.jpg)

Now... I don't really *need* touch ability to use it as a GPG key, but it would be nice if it worked... Wonder if it'd work if I soldered a wire to the pad?  Turns out, yes!

[![soldered](/pics/framework-yubi/soldered.jpg)](/pics/framework-yubi/soldered.jpg)

For my first try I just skinned a tiny hole in the wire, and it worked *ok* but I ended up having to push really hard to make contact.  I ended up skinning the entire wire and now any light touch works perfectly.

[![pre-install](/pics/framework-yubi/pre-install.jpg)](/pics/framework-yubi/pre-install.jpg)

One more problem to solve... Suddenly my yubikey was being pressed without me touching it, I had checked if the aluminum-looking body of the laptop or the modules were conductive with a multimeter before and got 0 ohms, but turns out when you push a wire really hard into it, it's enough to trigger the yubikey sensor.  That's why in the pic of it installed in the laptop up top, you can see only the middle is exposed, I put 2 bits of electrical tape on each side where it touches the body of the expansion card.

Overall, I'm very happy with this. For questions/comments, please reply to the [fediverse post](https://moparisthe.best/notice/AgbCUJdgcCKV57rpke).
