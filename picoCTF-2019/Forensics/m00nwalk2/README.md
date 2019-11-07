# m00nwalk2

__Problem__

Revisit the last transmission. We think this transmission contains a hidden message. There are also some clues clue 1, clue 2, clue 3. You can also find the files in /problems/m00nwalk2_0_c513cbf9ae6c76876372b8e29826e77b.

__Hint__

Use the clues to extract the another flag from the .wav file

__Solution__

Please revisit m00nwalk(the first part) for a detailed explanation on how it works.
Plugging in all the three `.wav` files into QSSTV, we get the following messages.
```
Password hidden_stegosaurus
The quieter you are the more you can HEAR
Alan Eliasen the FutureBoy
```
Searching for "Alan Eliasen the Future Boy" brings us to [this  page](https://futureboy.us/stegano/), which talks about Steganography Tools.

> These pages use the steghide program to perform steganography, and the files generated are fully compatible with steghide.

So, let's use `steghide` to try and recover a hidden message from the original file:

```bash
$ steghide extract -sf message.wav -p hidden_stegosaurus
wrote extracted data to "steganopayload12154.txt".
$ cat steganopayload12154.txt
picoCTF{the_answer_lies_hidden_in_plain_sight}
```

__Flag__

picoCTF{the_answer_lies_hidden_in_plain_sight}
