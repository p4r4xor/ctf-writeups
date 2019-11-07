# plumbing

__Problem__

> Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to 2019shell1.picoctf.com 18944.

__Hint__

> Remember the flag format is picoCTF{XXXX}

> What's a pipe? No not that kind of pipe... This [kind](http://www.linfo.org/pipes.html)

__Solution__

This is basicallly a combination of [net cat](../net%20cat/) and [grep 1](../grep%201).
```
$ nc 2019shell1.picoctf.com 18944 | grep picoCTF
```

__FLAG__ 

> picoCTF{digital_plumb3r_931b2271}
