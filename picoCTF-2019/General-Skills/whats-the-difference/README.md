# whats-the-difference

__Problem__

> Can you spot the difference? [kitters](kitters.jpg) [cattos](cattos.jpg). They are also available at /problems/whats-the-difference_0_00862749a2aeb45993f36cc9cf98a47a on the shell server

__Hint__

> How do you find the difference between two files?

> Dumping the data from a hex editor may make it easier to compare.

__Solution__

Given the hints, we need to find the difference between the files while dumping the hex of it.
The first way is to manually do it, the second being the automated.

```
diff <(xxd kitters.jpg) <(xxd cattos.jpg)
```
(or) we can run this python script.

```
with open('./kitters.jpg', 'rb') as f:
  kitters = f.read()

with open('./cattos.jpg', 'rb') as f:
  cattos = f.read()

flag = ''
for i in range(min(len(kitters), len(cattos))):
  if kitters[i] != cattos[i]:
    flag += cattos[i]
print flag
```


__Flag__

> picoCTF{th3yr3_a5_d1ff3r3nt_4s_bu773r_4nd_j311y_aslkjfdsalkfslkflkjdsfdszmz10548}`
