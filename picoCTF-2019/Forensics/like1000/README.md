# like100

__Problem__

> This .tar file got tarred alot. Also available at /problems/like1000_0_369bbdba2af17750ddf10cc415672f1c.

__HINT__

> Try and script this, it'll save you alot of time

__SOLUTION__

Given a .tar file, we need to extract the following contents. This can be done the following.
```console
$ tar -xvf 1000.tar
999.tar
filler.txt
$ tar -xvf 999.tar
998.tar
filler.txt
```
I guess by now, you'd know what's happening. It isn't feasable for us to extract a 1000 times by hand, gotta write a script.
```bash
#!/bin/bash

for ((i = 1000; i > 0; i--)); do
    if [ ! -f "$i.tar" ]; then
        break
    fi
    tar -xvf $i.tar
    rm $i.tar
done

```

After running the above script, we'll get a PNG file which contains the flag.


__Flag__

picoCTF{l0t5_0f_TAR5}
