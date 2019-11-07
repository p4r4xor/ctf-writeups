# First Grep

__Problem__

> Can you find the flag in [file](file)? This would be really tedious to look through manually, something tells me there is a better way. You can also find the file in /problems/first-grep_3_2e09f586a51352180a37e25913f5e5d9 on the shell server.

__Hint__

> grep [tutorial](https://ryanstutorials.net/linuxtutorial/grep.php)

__Solution__

Run
```console
grep "picoCTF" file
```
Basically you are asking the `grep` command to find a string `picoCTF` in a `file`

__Flag__

> picoCTF{grep_is_good_to_find_things_eda8911c}
