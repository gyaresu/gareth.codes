---
layout: post
title:  "Debugging a Silicon Labs EFM8 µC via an EFM8 Starter Kit"
date:   2016-12-13 14:51:00
categories: hacking, technology, embedded, efm8
published: false
tags: technology, programming, efm8, cc11xx, siliconlabs
---

## Programming an EFM8 microcontroller ([µC][micro])

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">External flashing and debugging now working on the <a href="https://twitter.com/hashtag/Boldport?src=hash">#Boldport</a> &#39;Touchy&#39; <a href="https://twitter.com/hashtag/EFM8?src=hash">#EFM8</a> capacitive touch board.<a href="https://twitter.com/hashtag/embedded?src=hash">#embedded</a> <a href="https://twitter.com/hashtag/rfcat?src=hash">#rfcat</a> <a href="https://twitter.com/hashtag/hackrf?src=hash">#hackrf</a> <a href="https://t.co/SSDP9juxFY">pic.twitter.com/SSDP9juxFY</a></p>&mdash; ☞ Gareth (@gareth__) <a href="https://twitter.com/gareth__/status/808749553918693376">December 13, 2016</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<!--more-->

# M'kay, why?

Back in July 2016 I was listening to a [podcast][podcast] from [Macrofab][macrofab], and [Parker Dillman][lnghrn] mentioned he'd just finished version two of a watch that uses LEDs as a binary display.

The first [MacroWatch][macrov1] was based on a PIC microcontroller and I was really interested in how the new V2 got x5 better battery life by using the EFM8 µC.

 - [MacroWatchV2][macrov2]

Seeing as the MacroWatchV2 was licenced [CC BY-SA 4.0][cc4] I uploaded the [MacroWatchV2 boards][oshproject] as an OSHPark Shared Project and ordered a set of three.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/siliconlabs">@siliconlabs</a> Any links on how to programme an EFM8 board using SleepyBee &amp; Simplicity Studio or not possible? /cc <a href="https://twitter.com/boldport">@boldport</a> Thanks! <a href="https://twitter.com/hashtag/lazyweb?src=hash">#lazyweb</a></p>&mdash; ☞ Gareth (@gareth__) <a href="https://twitter.com/gareth__/status/765650988027944960">August 16, 2016</a></blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Then I ordered a free sample of the [EFM8SB10F2G-A-QFN20][sample]... and figured I'd sort the rest out when I had some more time.

In the meantime I'd been seeing more and more of [Boldport Club][bc] on Twitter and [Saar][saar] mentioned he was prototyping a capacitive touch board called [Touchy][touchy].

After having seen the consistently high quality of his first projects it now seemed like a great time to grab myself a membership.

Saar ended up being the one who told me about all recent EFM8's coming with a default bootloader, enabling one to flash the firmware via only serial and not need the proprietary C2 serial two-wire setup.

It can take projects a long time to come together. When one is learning new skills, thinking things through in the shower is a helpful way of piecing a lot of contradictory or related parts together into a half-decent game-plan. 

Swimming around in ignorance is a very comfortable place for me. I love the challenge of being clueless and having to learn a lot to accomplish projects with limited assistance. 

So a month later I kinda-sorta thought that perhaps an EFM8 Development ('Starter') Board would be able to programme the MacroWatch2 via its onboard debugger. So I bought one for CA$44 (as part of a >$100 order for free shipping) from Mouser.

The board went into one of my 'boxes of parts that might come in handy at some point'.

At some point around then I grabbed a Hakko FX-888D solder station that popped up on craigslist. 

Skip forward another chunk-o-time to a quite evening where I sat down with all the best intentions of hand soldering the 0604 components onto the OSHPark MacroWatch board.

Let's just say that it's quite disconcerting to be looking through a magnifying glass, unable to determine if you're looking at an empty solder pad or the top of resistor.

They're just *_that_* small.

![MacroWatchv2 Hand soldering][hand]

That then lead me to buying a hot air rework station, with the idea in mind that I would use a soft syringe solder paste and manually apply it to the remaining parts.

Needless to say the unevenness of the solder caused some problems with consistency and volume but it was certainly a lot more successful.

That was a couple weeks ago and one of the reasons I still hadn't really got motivated to attempt finishing the board is that I had no way of connecting the board to the debugger.

![Plug'o'nails TC2030 from Tag-Connect][nails]

You'll notice that the entire interface from programming the MacroWatchV2 takes up no more space than an 0805 part...

Not exactly a lot of surface area to solder on patch wires, which was the least terrible plan I kept coming back to in the shower.

Why not just use the super awesome looking six-legged pogo-pin cable that it was meant to take?

Great question!

![TC2030-IDC-NL][pogo]

You see, the Tag-Connect [TC2030-IDC-NL][tc2030] was only available directly from their website and shipping to Canada was the dreaded CA$50 that you see from suppliers who have made _completely legitimate business decisions_ why they'd rather make you pay for USA Fedex than deal with the hassles of $5 shipping via USPS Standard First Class Mail like OSHPark does.

Even if it's just a _**cable**_.


\<--- _insert unrelated [Breakfast Club][breakfast] GIF here_ --->

![molly][molly]

_**"Thanks Obama :("**_

Fun side-note, this is exactly the reason I didn't just order a binary watch from MacroFab's own service. $10 board? Sure! $50 postage. Have a Nice Day!

While it always feels good to have a rant about the injustices of international shipping cost, no-one made me use these damn parts.

Y'know, some of these damn parts were created _**for free**_ and shared via an Open Source license so that muppets like me can make a dogs breakfast of putting them together.

I knew early on that this little project was going to take doubling down on parts and tooling which I would need to purchase.

And honestly, I'm ok with that. This is definitely not another damn Arduino project.

![Blinking an LED with Arduino][blinky]



I had a look at the Silicon Labs IDE called [Simplicy Studio v4][ss] and the range of dev boards  



<hr>

<br />

#### Current interests:
* [Silicon Labs EFM8][efm8]
  * [MacroWatchv2][macrov2]
  * [Boldport Club - Touchy][touchy]
  * [Silicon Labs EFM8SB1 Starter Kit][sleepy]
* [Kickstarter: 1Bitsy & Black Magic Probe — Cortex-M4F development platform and debugger][bmp]

[bmp]:              https://www.kickstarter.com/projects/esden/1bitsy-and-black-magic-probe-demystifying-arm-prog
[efm8]:             https://www.silabs.com/products/mcu/8-bit/Pages/8-bit-microcontrollers.aspx
[sleepy]:           https://www.silabs.com/products/mcu/8-bit/pages/efm8-sleepy-bee-starter-kits.aspx
[oshproject]:       https://oshpark.com/shared_projects/1hTj9Fo3       
[sample]:           https://www.silabs.com/products/mcu/8-bit/efm8-sleepy-bee/pages/EFM8SB10F2G-QFN20.aspx
[hand]:             /files/hand.jpg
[molly]:            /files/molly.gif
[podcast]:         https://macrofab.com/blog/mep-ep25-lousy-datasheet-buyouts/
[simplicity]:       http://www.silabs.com/products/mcu/Pages/simplicity-studio.aspx
[nails]:            /files/nails.png
[cc4]:              https://creativecommons.org/licenses/by-sa/4.0/
[tc2030]:           http://www.tag-connect.com/TC2030-IDC-NL
[lnghrn]:           http://twitter.com/LnghrnEngineer
[micro]:            https://en.wikipedia.org/wiki/Microcontroller
[macrofab]:         https://macrofab.com
[macrov1]:          https://github.com/MacroFab/Macro_Watch
[macrov2]:          https://github.com/MacroFab/Macro_Watch_V2            
[breakfast]:        https://www.rottentomatoes.com/m/breakfast_club
[pogo]:             /files/pogo.jpg
[bc]:               http://www.boldport.club
[touchy]:           https://boldport.com/touchy
[saar]:             https://twitter.com/saardrimer
[cc1101]:           http://www.ti.com/product/cc1101
[rf1101]:           /files/saleae-rf1101se.jpg
[ys1]:              https://github.com/greatscottgadgets/yardstick/wiki/YARD-Stick-One
[teensy]:           https://www.pjrc.com/teensy/teensy31.html
[pjrc]:             https://www.pjrc.com
[order]:            http://store.oshpark.com/products/teensy-3-1
[oshpark]:          https://oshpark.com

