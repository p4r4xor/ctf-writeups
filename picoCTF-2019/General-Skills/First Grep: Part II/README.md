# First Grep: Part II

__PROBLEM__

Can you find the flag in /problems/first-grep--part-ii_0_b68f6a4e9cb3a7aad4090dea9dd80ce1/files on the shell server? Remember to use grep.

__HINT__

grep [tutorial](https://ryanstutorials.net/linuxtutorial/grep.php)

__SOLUTION__

We need to use grep recursively here. `grep -r` does the job.
```
grep -r pico
```

FLAG - `picoCTF{grep_r_to_find_this_0e28f3ee}`
