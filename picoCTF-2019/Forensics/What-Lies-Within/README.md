# What Lies Within

__Problem__

Theres something in the [building](buildings.png). Can you retrieve the flag?

__Hint__

There is data encoded somewhere, there might be an online decoder.

__Solution__

I didn't want to use the online decoder thing, which leads me to finding something deeply hidden within the file. Maybe something like altering the bits? Tried zsteg and worked like magic!
```bash
$ gem install zsteg
$ zsteg buildings.png
b1,r,lsb,xy         .. text: "^5>R5YZrG"
b1,rgb,lsb,xy       .. text: "picoCTF{h1d1ng_1n_th3_b1t5}"
b1,abgr,msb,xy      .. file: PGP Secret Sub-key -
b2,b,lsb,xy         .. text: "XuH}p#8Iy="
b3,abgr,msb,xy      .. text: "t@Wp-_tH_v\r"
b4,r,lsb,xy         .. text: "fdD\"\"\"\" "
b4,r,msb,xy         .. text: "%Q#gpSv0c05"
b4,g,lsb,xy         .. text: "fDfffDD\"\""
b4,g,msb,xy         .. text: "f\"fff\"\"DD"
b4,b,lsb,xy         .. text: "\"$BDDDDf"
b4,b,msb,xy         .. text: "wwBDDDfUU53w"
b4,rgb,msb,xy       .. text: "dUcv%F#A`"
b4,bgr,msb,xy       .. text: " V\"c7Ga4"
b4,abgr,msb,xy      .. text: "gOC_$_@o"
```
Well, you can see that the flag is hidden at `b1,rgb,lsb,xy`, which means that its at `bits 2, channel rgb, lsb, order xy`. What we need to be focusing here is the `lsb` part. `lsb` is called "least significant bit". More will be discussed about this in my upcoming picoCTF write-ups (the ones which have more points).
There's your flag :)

__Flag__ 

picoCTF{h1d1ng_1n_th3_b1t5}
