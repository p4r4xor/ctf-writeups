# What's A Net Cat?

__Problem__

> Using netcat (nc) is going to be pretty important. Can you connect to 2019shell1.picoctf.com at port 4158 to get the flag?

__Hint__

> nc [tutorial](https://linux.die.net/man/1/nc)

__Solution__

All you have to do is use netcat to connect to the given service on a given port:
```bash
$ nc 2019shell1.picoctf.com 4158
You're on your way to becoming the net cat master
picoCTF{nEtCat_Mast3ry_700da9c7}
```

__Flag__ 

> picoCTF{nEtCat_Mast3ry_700da9c7}
