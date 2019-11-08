# Investigative Reversing 0

__Problem__

> We have recovered a [binary](mystery) and an [image](mystery.png). See what you can make of it. There should be a flag somewhere. Its also found in /problems/investigative-reversing-0_0_ebc669df876196bdc09a2f54fd5fffed on the shell server.

__Hint__

> Try using some forensics skills on the image

> This problem requires both forensics and reversing skills

> A hex editor may be helpful

__Solution__

We're down to the main challenges now! Let's do this!
We're given a binary file and an image, let us first reverse the following code using `Ghidra`.

```C
int __cdecl main(int argc, const char **argv, const char **envp)
{
  signed int i; // [rsp+4h] [rbp-4Ch]
  signed int j; // [rsp+8h] [rbp-48h]
  FILE *stream; // [rsp+10h] [rbp-40h]
  FILE *v7; // [rsp+18h] [rbp-38h]
  char ptr; // [rsp+20h] [rbp-30h]
  char v9; // [rsp+21h] [rbp-2Fh]
  char v10; // [rsp+22h] [rbp-2Eh]
  char v11; // [rsp+23h] [rbp-2Dh]
  char v12; // [rsp+24h] [rbp-2Ch]
  char v13; // [rsp+25h] [rbp-2Bh]
  char v14; // [rsp+2Fh] [rbp-21h]
  unsigned __int64 v15; // [rsp+48h] [rbp-8h]

  v15 = __readfsqword(0x28u);
  stream = fopen("flag.txt", "r");
  v7 = fopen("mystery.png", "a");
  if ( !stream )
    puts("No flag found, please make sure this is run on the server");
  if ( !v7 )
    puts("mystery.png is missing, please run this on the server");
  if ( (signed int)fread(&ptr, 0x1AuLL, 1uLL, stream) <= 0 )
    exit(0);
  puts("at insert");
  fputc(ptr, v7);
  fputc(v9, v7);
  fputc(v10, v7);
  fputc(v11, v7);
  fputc(v12, v7);
  fputc(v13, v7);
  for ( i = 6; i <= 14; ++i )
    fputc((char)(*(&ptr + i) + 5), v7);
  fputc((char)(v14 - 3), v7);
  for ( j = 16; j <= 25; ++j )
    fputc(*(&ptr + j), v7);
  fclose(v7);
  fclose(stream);
  return __readfsqword(0x28u) ^ v15;
}
```
What happens in the above code is, from `i=6 to 14` bytes, they are added by `5`. 
The `i=15`th byte is subracted by 3. The rest of the code has nothing to do with the problem now.
Now, opening the image in an hex editor, we can see that some text is appended at the end.

```bash
0001e850: 8220 0882 2008 8220 6417 ffef fffd 7f5e  . .. .. d......^
0001e860: ed5a 9d38 d01f 5600 0000 0049 454e 44ae  .Z.8..V....IEND.
0001e870: 4260 8270 6963 6f43 544b 806b 357a 7369  B`.picoCTK.k5zsi
0001e880: 6436 715f 6662 3639 6636 6332 7d         d6q_fb69f6c2}
```
From the above script, we can see that the changes take place from the 6th byte onwards. Which starts from `K` in the malformed flag.

```python
data = picoCTK.k5zsid6q_fb69f6c2}
data = bytearray(data)

for i in range(6, 15):
  data[i] -= 5

data[15] += 3

print data
```
After running the above script, we'll get our flag :).

__Flag__

> picoCTF{f0und_1t_eeaec48b}

