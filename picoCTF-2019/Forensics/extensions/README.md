# extensions

__Problem__

> This is a really weird text file [TXT](flag.txt)? Can you find the flag?

__HINT__

>How do operating systems know what kind of file it is? (It's not just the ending!
>Make sure to submit the flag as picoCTF{XXXXX}

__Solution__

From the following hints, we can see that we need to find what kind of file it is. Well, one can argue the the extension is .txt! What's wrong with that? Well, point to be noted.
```
EXTENSIONS ARE A LIE.
```
Why? because they do not exactly reveal what kind of file it is. One can find what kind of file it is by running the following commands.
```
$xdg-open flag.txt

```
Did you get an error? Why? That's because it isn't a .txt extension :)
try the following.
```
$file flag.txt
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
```
lol what? how did this happen? Well, one needs to know that the type of file depends on the hex data of the file. These are called `Magic Bytes`. I'll be explaining about this more in the upcoming write-ups.

How do I convert the extension now? Do the following :)
```
$convert flag.txt flag.png
$xdg-open flag.png
```
and there resides your flag :)

__Flag__

picoCTF{now_you_know_about_extensions}
