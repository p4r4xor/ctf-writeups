# mus1c

__PROBLEM__

I wrote you a [song](lyrics.txt). Put it in the picoCTF{} flag format

__HINT__

Do you think you can master rockstar?

__SOLUTION__

The given text file is written in the esoteric language [rockstar](https://codewithrockstar.com/). You can run it over [here](https://codewithrockstar.com/online)
```
Output:
114
114
114
111
99
107
110
114
110
48
49
49
51
114

```
The following numbers are in decimal and gives us the flag when converted to ASCII.

```
$ python
>>> '''114
... 114
... 114
... 111
... 99
... 107
... 110
... 114
... 110
... 48
... 49
... 49
... 51
... 114'''.strip().split('\n')
['114', '114', '114', '111', '99', '107', '110', '114', '110', '48', '49', '49', '51', '114']
>>> ''.join(map(chr,map(int,_)))
'rrrocknrn0113r'

```

FLAG - `picoCTF{rrrocknrn0113r}`
