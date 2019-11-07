# unzip

__Problem__

> Can you unzip this [file](flag.zip) and get the flag?

__Hint__

> put the flag in the format picoCTF{XXXXX}

__Solution__

The title says to unzip the given file. The following does this.
```bash
$ unzip flag.zip
$ xdg-open flag.png
```
xdg-open lets you open files from the terminal instead of manually clicking it.
The flag is inside the png.

__Flag__

> picoCTF{unz1pp1ng_1s_3a5y}
