# where-is-the-file

__PROBLEM__

I’ve used a super secret mind trick to hide this file. Maybe something lies in /problems/where-is-the-file_4_f26b413d005c16c61f127740ab242b35. (The file is on their shell)

__HINT__

What command can see/read files?
What's in the manual page of ls?

__SOLUTION__

Hidden files are not shown by default by using `ls` on unix systems. We'll be using the `-a` option to show all of them.

```
$ ls -a
.  ..  .cant_see_me
$ cat .cant_see_me
picoCTF{w3ll_that_d1dnt_w0RK_cb4a5081}

```
(or)

```
$ ls -ld .*
```


FLAG - `picoCTF{w3ll_that_d1dnt_w0RK_cb4a5081}`
