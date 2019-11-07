# unzip

__PROBLEM__

Can you unzip this file and get the flag?

__HINT__

put the flag in the format picoCTF{XXXXX}

__SOLUTION__

The title says to unzip the given file. The following does this.
```bash
$ unzip flag.zip
$ xdg-open flag.png
```
xdg-open lets you open files from the terminal instead of manually clicking it.
The flag is inside the png.

FLAG - picoCTF{unz1pp1ng_1s_3a5y}
