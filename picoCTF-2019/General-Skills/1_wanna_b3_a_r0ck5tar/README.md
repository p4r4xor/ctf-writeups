# 1_wanna_b3_a_r0ck5tar

__Problem__

> I wrote you another [song](lyrics.txt). Put the flag in the picoCTF{} flag format

__Hint__

> None.

__Solution__

The given text file is written in the esoteric language [rockstar](https://codewithrockstar.com/). You can run it over [here](https://codewithrockstar.com/online). You need to remove the following lines to run it properly. 

```
Listen to the music             
If the music is a guitar                  
Say "Keep on rocking!"                
Listen to the rhythm
If the rhythm without Music is nothing
...
Else Whisper "That ain't it, Chief"

```

and you'll get the following output.

```
Output:
66
79
78
74
79
86
73

```
The following numbers are in decimal and gives us the flag when converted to ASCII.

```
$ python
>>> ''.join(map(chr,[66,79,78,74,79,86,73]))
'BONJOVI'

```

__FLAG__

> picoCTF{BONJOVI}
