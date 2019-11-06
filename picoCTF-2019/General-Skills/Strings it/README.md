# Strings it

__PROBLEM__

Can you find the flag in [file](strings) without running it? You can also find the file in /problems/strings-it_3_8386a6aa560aecfba03c0c6a550b5c51 on the shell server.

__HINT__

[strings](https://linux.die.net/man/1/strings)

__SOLUTION__

Using the `strings` on the file will give you lot of String but we only want the flag so we do something like
```
strings strings | grep "picoCTF"
```

FLAG - `picoCTF{5tRIng5_1T_c7fff9e5}`
