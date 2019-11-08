# pastaAAA

__Problem__

> This pasta is up to no good. There MUST be something behind it.

__Hint__

> None.


__Solution__

We've given a .png file, and the description says that there's something behind it.
One could think that there's an embedded file, but going through the hex shows nothing.
Being played a lot of CTFs, I've used tools from my stego toolkit, and Stegsolve has given me the answer.

The flag is hidden in the RGB-0,1 planes.

__Flag__

> picoCTF{pa$ta_1s_lyf3}