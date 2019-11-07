# So Meta

__PROBLEM__

I stopped using YellowPages and moved onto WhitePages... but the page they gave me is all blank!

__HINT__

None.

__SOLUTION__

No hints. This challenge would be a pain in the ass for newbies. But yet :v lets move on.
Given a text file (make sure it's a text file first), I've done `cat whitepages.txt` but no avail.
`EMPTY`
But one could comeup with an idea. We know that there is some text over here. But we couldn'ot see it. Remember the ASCII table? Each letter we know had a Decimal form, Hexadecimal form. Got an idea? Lets see.

```python
>>>"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                ".encode("hex")
'e28083e28083e28083e2808320e2808320e28083e28083e28083e28083e2808320e28083e2808320e28083e28083e28083e2808320e28083e2808320e28083202020e28083e28083e28083e28083e280832020e2808320e28083e2808320e280832020e28083e28083e28.........'
```
One could see that its some sort of repeating text. Well, you are partially correct and wrong.
We have the standard space `(0x20)`, and the Unicode `EM SPACE (U+2003 / 0xE2 0x80 0x83)`.
As there are only two types of unicode, let's treat the following as binary.
We can write a script to automate the process :)

```python
from pwn import *

with open("whitepages.txt", "rb") as binary:
    ans = bytearray(binary.read()) 
    ans = data.replace(b'\xe2\x80\x83', b'0')
    ans = data.replace(b'\x20', b'1')
    ans = data.decode("ascii")
    print unbits(ans)
```
pwntools is a library specially made for CTF purposes. Have fun installing it :p
If you couldn't, open the file in a text editor and `find and replace` the `\x20` with `1` and `\xe2\x80\x83` with `0`.
Running the following script gives you the flag :)

FLAG - picoCTF{not_all_spaces_are_created_equal_f006c045f6b402ce4bc749dc7a262380}
