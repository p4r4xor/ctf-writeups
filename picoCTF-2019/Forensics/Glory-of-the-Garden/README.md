# Glory of the Garden

__Problem__

> This [garden](garden.jpg) contains more than it seems. You can also find the file in /problems/glory-of-the-garden_3_346e50df4a37bcc4aa5f6e5831604e2a on the shell server.

__Hint__

> What is a hex editor?

__Solution__

Given the hint that we should be using a hex editor, open the image in one :stuck_out_tongue_closed_eyes:
I'd recommend `ghex` as it's very user friendly for beginners.
```
$ sudo apt-get install ghex
...
...
$ ghex garden.jpg
```
and find your flag by scanning the whole hex dump :blush: or you could use strings to find the flag.

```
$ strings garden.jpg
...
Here is a flag "picoCTF{more_than_m33ts_the_3y35a97d3bB}"
```
__Flag__ 

> picoCTF{more_than_m33ts_the_3y35a97d3bB}
