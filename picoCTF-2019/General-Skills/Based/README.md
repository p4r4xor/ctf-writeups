# Based

__Problem__

> To get truly 1337, you must understand different data encodings, such as hexadecimal or binary. Can you get the flag from this program to prove you are on the way to becoming 1337? Connect with nc 2019shell1.picoctf.com 20836.

__Hint__

> I hear python can convert things.

> It might help to have multiple windows open

__Solution__

All you have to do is decode base2, base8 and base64 data. The following script will help a lot or you can do it by using online decoders.
```python
from pwn import *

sh = remote('2019shell1.picoctf.com', 20836)

binary_data = sh.recvuntil('Input:\n').split('\n')[2].split(' ')[3:-3]
binary_data = ''.join(map(lambda x: chr(int(x, 2)), binary_data))
sh.sendline(binary_data)

oct_data = sh.recvuntil('Input:\n').split('\n')[0].split('the  ')[-1].split(' as')[0].split(' ')
oct_data = ''.join(map(lambda x: chr(int(x, 8)), oct_data))
sh.sendline(oct_data)

hex_data = sh.recvuntil('Input:\n').split('\n')[0].split('the ')[-1].split(' as')[0]
hex_data = hex_data.decode('hex')
sh.sendline(hex_data)

sh.interactive()

```

__Flag__

> picoCTF{learning_about_converting_values_6cdcad0d}
