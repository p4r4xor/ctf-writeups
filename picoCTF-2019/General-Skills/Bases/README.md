# Bases

__Problem__

> What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.

__Hint__

Submit your answer in our competition's flag format. For example, if you answer was 'hello', you would submit 'picoCTF{hello}' as the flag.

__Solution__

Base64 is a very common encoding. As the Title suggests to go with bases, Base64 was the first to come up in my mind. To decode the following text, use an online Base64 decoder or use this.
Hit the following in the terminal to get your flag. Read the manual pages of echo and base64 for an indepth understanding.

```console
$ echo "bDNhcm5fdGgzX3IwcDM1" | base64 -d
```

__Flag__
> picoCTF{l3arn_th3_r0p35}
