# m00nwalk


__Problem__

> Decode this [message](message.wav) from the moon. You can also find the file in /problems/m00nwalk_4_bcf65d52e5462dd0b70c0e984d7d5015.

__Hints__

> How did pictures from the moon landing get sent back to Earth?
> What is the CMU mascot?, that might help select a RX option

__Solution__

Nothing meaningful can be identified listening to the file. Also visualizing the file didn't lead anywhere. The hint suggests that this is related to how images from the moon landing were transmitted back to earth. Some research leads to [SSTV](https://en.wikipedia.org/wiki/Slow-scan_television):

> Slow Scan television (SSTV) is a picture transmission method used mainly by amateur radio operators, to transmit and receive static pictures via radio in monochrome or color. 
> The Apollo TV cameras used SSTV to transmit images from inside Apollo 7, Apollo 8, and Apollo 9, as well as the Apollo 11 Lunar Module television from the Moon.

[This tutorial](https://ourcodeworld.com/articles/read/956/how-to-convert-decode-a-slow-scan-television-transmissions-sstv-audio-file-to-images-using-qsstv-in-ubuntu-18-04) explains how to use a program called `qsstv` to convert the audio files back to images.

In short:

```console
$ apt-get install qsstv
$ pactl load-module module-null-sink sink_name=virtual-cable
22
$ pavucontrol # A GUI will pop-up, go to the "Output Devices" tab to verify that you have the "Null Output" device
$ qsstv # The program GUI will pop-up, go to "Options" -> "Configuration" -> "Sound" and select the "PulseAudio" Audio Interface
$ # Back in the pavucontrol GUI, select the "Recording" tab and specify that QSSTV should capture audio from the Null Output
```

The hint asked "What is the CMU mascot?" - the answer is "Scotty the Scottie Dog". This hinted that we should select "Scottie 1" as QSSTV's "Mode". I also had to select "Auto Slant" via trial and error.

At this point we can click the "Play" button in QSSTV to start the receiver, and then play the audio file:
```console
$ paplay -d virtual-cable message.wav 
```

The image is received and decoded by the program:



After the transmission has ended, we can cleanup by using the following commands:

```console
$ pactl list short modules | grep null
22      module-null-sink        sink_name=virtual-cable
$ pactl unload-module 22
```
Thanks [David](https://github.com/Dvd848/)

__Flag__ 

> picoCTF{beep_boop_im_in_space}

