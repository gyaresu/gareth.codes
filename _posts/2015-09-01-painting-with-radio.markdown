---
layout: post
title:  "Painting with Radio"
date:   2015-09-01 007:13:00
categories: hacking, technology, sdr
published: true
tags: technology, programming, sdr
---

## HackRF Node Stream Spectrum Painter

Folks were playing around with [Hellschreiber](https://en.wikipedia.org/wiki/Hellschreiber) encoding in the #hackrf channel on Freenode last week using `hackrf_transfer`

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="en" dir="ltr">HackRF&#39;s tx/rx&#39;ing images in waterfall plots using <a href="http://t.co/Lyijkr63QP">http://t.co/Lyijkr63QP</a> <a href="http://t.co/JwLsO29dqC">http://t.co/JwLsO29dqC</a> <a href="https://twitter.com/hashtag/SDR?src=hash">#SDR</a> <a href="https://twitter.com/hashtag/HackRF?src=hash">#HackRF</a> <a href="http://t.co/aAKk4eLBgV">pic.twitter.com/aAKk4eLBgV</a></p>&mdash; ☞ Gareth (@gyaresu) <a href="https://twitter.com/gyaresu/status/634796029859131396">August 21, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Which then made me remember a tweet from @maxogden playing around with a `hackrf` `node` module at the [CCC](https://www.ccc.de/en/) 2015 camp.

And using a `hackrf` via `node` is something I've wanted since before it was even a `thing`.

<!--more-->

### Spectrum Painter 

#### Use [Spectrum Painter](https://github.com/polygon/spectrum_painter) to create an IQ stream:

```bash
python spectrum_painter/img2iqstream.py examples/gareth.png --samplerate 8000000 --format hackrf > gareth.raw
```

#### Then test with `hackrf_transfer`: 
```bash
hackrf_transfer -f 915000000 -s 3700000 -t gareth.raw -x 20
```

#### Show the transmission on a second machine with `gqrx`:
[GQRX](http://gqrx.dk) is a multi-platform software reciever with waterfall plot.

You might need to tweak some of the sample rate / fft settings in both `hackrf_transfer` & `gqrx` to get the correct aspect ratio but it's not difficult.

```
FFT: 8192
Rate: 50fps
Filter Width: Normal
Filter Shape: Normal
Mode: Narrow/FM
AGC: Fast
```

### HackRF for Node

#### So I wrote something straight from my brain using [hackrf-stream](https://github.com/mappum/hackrf-stream)...


```node
var devices = require('hackrf-stream')
var fs = require('fs')

var radio = devices(0).open(0)

radio.setFrequency(9.15e8)

radio.setSampleRate(3.7e6)

var tx = radio.createWriteStream()

fs.readFile('./gareth.raw', function (err, data) {
  if (err) {
    throw err
  }
  tx.write(data)
})
```

#### ... and it worked.

![First test](/files/gareth-hackrf-node-success.jpg)
_I managed to capture the very first code test. While in utter shock it actually worked!_



<hr>

<br />

#### Current interests:
 * What's old is new again
   * [macports](https://twitter.com/gyaresu/status/636768271337828352) > [homebrew](https://github.com/metacollin/homebrew-gnuradio)
   * [Macbook Pro](https://support.apple.com/kb/SP582): Mid 2010, 15", 2.66GHz, 8GB DDR3, NVIDIA GT 330M 512MB GDDR3
 * Tools
   * [rename](http://plasmasturm.org/code/rename/)
   * [iftop](https://en.wikipedia.org/wiki/Iftop)
 * [SDR » I/Q Data for Dummies](http://whiteboard.ping.se/SDR/IQ)
 * [OS X Yosemite security and privacy guide](https://github.com/drduh/OS-X-Yosemite-Security-and-Privacy-Guide)
 * [NodeSchool - learnyounode](https://github.com/workshopper/learnyounode)
 * [GoodFET](http://goodfet.sourceforge.net) - an open-source JTAG adapter
   * [Problems setting up the GoodFET](https://gist.github.com/gyaresu/7901e5a4a3348a5a2d37)
 * [YARD Stick One](http://greatscottgadgets.com/yardstickone/) by [@michaelossmann](https://twitter.com/michaelossmann)
 * [Linux workstation security checklist](https://github.com/lfit/itpol/blob/master/linux-workstation-security.md)
 * [Belkin F9K1111 V1.04.10 Firmware Analysis](http://blog.vectranetworks.com/blog/belkin-analysis)
 * [Introduction to _The Wikileaks Files_](http://gizmodo.com/gizmodo-exclusive-read-julian-assanges-introduction-to-1726605781) by [Julian Assange](https://en.wikipedia.org/wiki/Julian_Assange)
 * [Vestiges and Claws](https://en.wikipedia.org/wiki/Vestiges_and_Claws) - 2015 album by [José González](https://en.wikipedia.org/wiki/José_González_(singer))