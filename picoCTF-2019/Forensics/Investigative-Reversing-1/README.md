# Investigative Reversing 1

__Problem__

> We have recovered a binary and a few images: image, image2, image3. See what you can make of it. There should be a flag somewhere. Its also found in /problems/investigative-reversing-1_4_266adcde17fa2ab2ec454e6c5379ad81 on the shell server.

__Hint__

> Try using some forensics skills on the image

> This problem requires both forensics and reversing skills

> A hex editor may be helpful

__Solution__

We're given a binary file and an image, let us first reverse the following code using `Ghidra`.

```C
void main(void)

{
  long lVar1;
  FILE *flag_stream;
  FILE *m1_stream;
  FILE *m2_stream;
  FILE *m3_stream;
  long in_FS_OFFSET;
  char local_6b;
  int i;
  int j;
  int k;
  char flag [6];
  
  lVar1 = *(long *)(in_FS_OFFSET + 0x28);
  flag_stream = fopen("flag.txt","r");
  m1_stream = fopen("mystery.png","a");
  m2_stream = fopen("mystery2.png","a");
  m3_stream = fopen("mystery3.png","a");
  if (flag_stream == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (m1_stream == (FILE *)0x0) {
    puts("mystery.png is missing, please run this on the server");
  }
  fread(flag,26,1,flag_stream);
  fputc((int)flag[1],m3_stream);
  fputc((int)(char)(flag[0] + '\x15'),m2_stream);
  fputc((int)flag[2],m3_stream);
  local_6b = flag[3];
  fputc((int)flag[5],m3_stream);
  fputc((int)flag[4],m1_stream);
  i = 6;
  while (i < 10) {
    local_6b = local_6b + '\x01';
    fputc((int)flag[i],m1_stream);
    i = i + 1;
  }
  fputc((int)local_6b,m2_stream);
  j = 10;
  while (j < 0xf) {
    fputc((int)flag[j],m3_stream);
    j = j + 1;
  }
  k = 0xf;
  while (k < 0x1a) {
    fputc((int)flag[k],m1_stream);
    k = k + 1;
  }
  fclose(m1_stream);
  fclose(flag_stream);
  if (lVar1 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
```
The below shows that our flag is scattered between three images, and have them appended at the end after `IEND.B`

```bash
└──╼ $xxd mystery.png | tail
0001e7f0: 8220 0882 2008 8220 0882 2064 1f32 1221  . .. .. .. d.2.!
0001e800: 0882 2008 8220 0882 2008 42f6 2123 1182  .. .. .. .B.!#..
0001e810: 2008 8220 0882 2008 8220 641f 3212 2108   .. .. .. d.2.!.
0001e820: 8220 0882 2008 8220 0842 f621 2311 8220  . .. .. .B.!#.. 
0001e830: 0882 2008 8220 0882 2064 1f32 1221 0882  .. .. .. d.2.!..
0001e840: 2008 8220 0882 2008 42f6 2123 1182 2008   .. .. .B.!#.. .
0001e850: 8220 0882 2008 8220 6417 ffef fffd 7f5e  . .. .. d......^
0001e860: ed5a 9d38 d01f 5600 0000 0049 454e 44ae  .Z.8..V....IEND.
0001e870: 4260 8243 467b 416e 315f 3835 3536 3131  B`.CF{An1_855611
0001e880: 6433 7d                                  d3}

└──╼ $xxd mystery2.png | tail
0001e7e0: 2108 8220 0882 2008 8220 0842 f621 2311  !.. .. .. .B.!#.
0001e7f0: 8220 0882 2008 8220 0882 2064 1f32 1221  . .. .. .. d.2.!
0001e800: 0882 2008 8220 0882 2008 42f6 2123 1182  .. .. .. .B.!#..
0001e810: 2008 8220 0882 2008 8220 641f 3212 2108   .. .. .. d.2.!.
0001e820: 8220 0882 2008 8220 0842 f621 2311 8220  . .. .. .B.!#.. 
0001e830: 0882 2008 8220 0882 2064 1f32 1221 0882  .. .. .. d.2.!..
0001e840: 2008 8220 0882 2008 42f6 2123 1182 2008   .. .. .B.!#.. .
0001e850: 8220 0882 2008 8220 6417 ffef fffd 7f5e  . .. .. d......^
0001e860: ed5a 9d38 d01f 5600 0000 0049 454e 44ae  .Z.8..V....IEND.
0001e870: 4260 8285 73                             B`..s

└──╼ $xxd mystery3.png | tail
0001e7e0: 2108 8220 0882 2008 8220 0842 f621 2311  !.. .. .. .B.!#.
0001e7f0: 8220 0882 2008 8220 0882 2064 1f32 1221  . .. .. .. d.2.!
0001e800: 0882 2008 8220 0882 2008 42f6 2123 1182  .. .. .. .B.!#..
0001e810: 2008 8220 0882 2008 8220 641f 3212 2108   .. .. .. d.2.!.
0001e820: 8220 0882 2008 8220 0842 f621 2311 8220  . .. .. .B.!#.. 
0001e830: 0882 2008 8220 0882 2064 1f32 1221 0882  .. .. .. d.2.!..
0001e840: 2008 8220 0882 2008 42f6 2123 1182 2008   .. .. .B.!#.. .
0001e850: 8220 0882 2008 8220 6417 ffef fffd 7f5e  . .. .. d......^
0001e860: ed5a 9d38 d01f 5600 0000 0049 454e 44ae  .Z.8..V....IEND.
0001e870: 4260 8269 6354 3074 6861 5f              B`.icT0tha_

```

The following code reverses the binary to get us the flag.

```python
from pwn import *
part1 = unhex('43467b416e315f62313739313135657d')
part2 = unhex('8573')
part3 = unhex('696354307468615f')

out = bytearray('0'*0x1a)

out[1] = part3[0]
out[21] = part2[0]
out[2] = part3[1]
out[5] = part3[2]
out[4] = part1[0]

for i in range(6,10):
  out[i] = part1[i-5]

out[3] = chr(ord(part2[1])-4)

for i in range(10, 15):
  out[i] = part3[i-7]

for i in range(15,26):
  out[i] = part1[i-10]

print out
```
After running the above script, we'll get our flag :).

__Flag__

> picoCTF{An0tha_1_b179115e}