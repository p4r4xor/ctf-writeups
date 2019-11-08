# Investigative Reversing 2

__Problem__

> We have recovered a binary and an image See what you can make of it. There should be a flag somewhere. Its also found in /problems/investigative-reversing-2_0_f86bb3c9e3e3c1e49a431642c59796e2 on the shell server.

__Hint__

> Try using some forensics skills on the image

> This problem requires both forensics and reversing skills

> What is LSB encoding?

__Solution__

We're given a binary file and an image, let us first reverse the following code using `Ghidra`.

```C
ulong codedChar(int param_1,byte param_2,byte param_3)
{
  byte local_20;
  
  local_20 = param_2;
  if (param_1 != 0) {
    local_20 = (byte)((int)(char)param_2 >> ((byte)param_1 & 0x1f));
  }
  return (ulong)(param_3 & 0xfe | local_20 & 1);
}
undefined8 main(void)
{
  long lVar1;
  size_t sVar2;
  ulong uVar3;
  long in_FS_OFFSET;
  byte b;
  char local_7d;
  int bytes_read;
  int i;
  uint j;
  int k;
  undefined4 local_6c;
  int limit;
  int bytes_read_from_flag;
  FILE *flag_file;
  FILE *original_file;
  FILE *encoded_file;
  byte flag [50];
  
  lVar1 = *(long *)(in_FS_OFFSET + 0x28);
  local_6c = 0;
  flag_file = fopen("flag.txt","r");
  original_file = fopen("original.bmp","r");
  encoded_file = fopen("encoded.bmp","a");
  if (flag_file == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (original_file == (FILE *)0x0) {
    puts("No output found, please run this on the server");
  }
  sVar2 = fread(&b,1,1,original_file);
  bytes_read = (int)sVar2;
  limit = 0x2d3;
  i = 0;
  while (i < limit) {
    fputc((int)(char)b,encoded_file);
    sVar2 = fread(&b,1,1,original_file);
    bytes_read = (int)sVar2;
    i = i + 1;
  }
  sVar2 = fread(flag,50,1,flag_file);
  bytes_read_from_flag = (int)sVar2;
  if (bytes_read_from_flag < 1) {
    puts("Invalid Flag");
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  j = 0;
  while ((int)j < 100) {
    if ((j & 1) == 0) {
      k = 0;
      while (k < 8) {
        uVar3 = codedChar(k,flag[(int)j / 2],b);
        local_7d = (char)uVar3;
        fputc((int)local_7d,encoded_file);
        fread(&b,1,1,original_file);
        k = k + 1;
      }
    }
    else {
      fputc((int)(char)b,encoded_file);
      fread(&b,1,1,original_file);
    }
    j = j + 1;
  }
  while (bytes_read == 1) {
    fputc((int)(char)b,encoded_file);
    sVar2 = fread(&b,1,1,original_file);
    bytes_read = (int)sVar2;
  }
  fclose(encoded_file);
  fclose(original_file);
  fclose(flag_file);
  if (lVar1 == *(long *)(in_FS_OFFSET + 0x28)) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}
```
As you can see from the decompiled code, `limit = 0x2d3` means that the encoding starts from `0x2d3`. 
The following script will give us the flag.

```python
with open('./encoded.bmp', 'rb') as f:
  data = f.read()

data = data[2000:2000+(50*8)]

out = ''

for i in range(50):
  c = 0
  for j in range(8):
    c = c | (ord(data[i*8+(7-j)])&1)
    c = c << 1
  c = c >> 1
  out += chr(c+5)
  print c
  print out
```

The following code reverses the binary to get us the flag.

__Flag__

> picoCTF{n3xt_0n30000000000000000000000000f69eb8c8}