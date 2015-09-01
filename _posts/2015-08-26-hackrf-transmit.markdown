---
layout: post
title:  "WBFM Transmit with HackRF & GNURadio"
date:   2015-08-26 15:19:00
categories: hacking, technology, sdr
published: true
tags: technology, programming, sdr, hackrf, radio, iot
---

## Radio transmissions with HackRF

Today I was transmitting a 'Wide Band Frequency Modulation' ([WBFM](https://en.wikipedia.org/wiki/Frequency_modulation)) encoded radio in a carrier wave with [Michael Ossmann's]() Software Defined Radio ([SDR]()) peripheral, [HackRF](https://greatscottgadgets.com/hackrf/).

I leave my experience here as breadcrumbs for others who follow in the path of learning Digital Signal Processing ([DSP](https://en.wikipedia.org/wiki/Digital_signal_processing))

<!--more-->

### GNURadio Companion file:
WBFM Transmit with HackRF & GNURadio: [HackRF-FM-Transmit.grc](https://gist.github.com/gyaresu/343ae51ecbb70486e270)

### Streaming audio

Using a [named pipe](https://en.wikipedia.org/wiki/Named_pipe) as a way to control the sample rate of our broadcast source (in this case) of a streaming internet radio station.

`$ mkfifo stream_32k.fifo`

`$ mpg123 -r32000 -m -s http://maxxima.mine.nu:8000 > stream_32k.fifo`

```
$ mpg123
You made some mistake in program usage... let me briefly remind you:

High Performance MPEG 1.0/2.0/2.5 Audio Player for Layers 1, 2 and 3
        version 1.22.4; written and copyright by Michael Hipp and others
        free software (LGPL) without any warranty but with best wishes

usage: mpg123 [option(s)] [file(s) | URL(s) | -]
supported options [defaults in brackets]:
   -v    increase verbosity level       -q    quiet (don't print title)
   -t    testmode (no output)           -s    write to stdout
   -w f  write output as WAV file
   -k n  skip first n frames [0]        -n n  decode only n frames [all]
   -c    check range violations         -y    DISABLE resync on errors
   -b n  output buffer: n Kbytes [0]    -f n  change scalefactor [32768]
   -r n  set/force samplerate [auto]
   -o m  select output module           -a d  set audio device
   -2    downsample 1:2 (22 kHz)        -4    downsample 1:4 (11 kHz)
   -d n  play every n'th frame only     -h n  play every frame n times
   -0    decode channel 0 (left) only   -1    decode channel 1 (right) only
   -m    mix both channels (mono)       -p p  use HTTP proxy p [$HTTP_PROXY]
   -@ f  read filenames/URLs from f
   -z    shuffle play (with wildcards)  -Z    random play
   -u a  HTTP authentication string     -E f  Equalizer, data from file
   -C    enable control keys            --no-gapless  not skip junk/padding in mp3s
   -?    this help                      --version  print name + version
See the manpage mpg123(1) or call mpg123 with --longhelp for more parameters and information.
```

### Transmit (TX): Using [GNURadio Companion (GRC)](http://gnuradio.org/redmine/projects/gnuradio/wiki/GNURadioCompanion)
<iframe src="https://player.vimeo.com/video/137431112" width="500" height="313" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>



### Recieve (RX): Using [GQRX](http://gqrx.dk)
<iframe src="https://player.vimeo.com/video/137431075" width="500" height="313" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>



<hr>

<br />

#### Current interests:

 * [GNURadio](http://gnuradio.org)
   * [Live-stream](https://www.youtube.com/watch?v=r64-EA0IneU) from [GNURadio Conf 2015](http://www.trondeau.com/gnu-radio-conference-2015/)