# shark on wire 1

__Problem__

> We found this packet [capture](capture.pcap). Recover the flag. You can also find the file in /problems/shark-on-wire-1_0_13d709ec13952807e477ba1b5404e620.

__Hint__

> Try using a tool like Wireshark

> What are streams?

__Solution__

Looks like a new extension huh? `.pcap`. These kind of files can be opened by using tools like wireshark or tshark (just don't forget to do the `file` command on the given files before diving in!). 

Installing wireshark:
```
$ sudo apt-get install wireshark
$ sudo dpkg-reconfigure wireshark-common
$ sudo adduser $USER wireshark
$ wireshark
```
To open the file in wireshark, do the following.
```
$ wireshark capture.pcap
```
Once you open the file, you can see random things which you perhaps might not understand :p
Well, these are network packets captured between some communication. 
wireshark records and collects all the packets between the communication. 
Each packet is shown in the following way -- Number of the packet, Time recorded, Source IP, Destination IP, Protocol Used, Length of the recorded packet and info of the packet.
Now, the second hint says that we need to follow a "stream".
What's a wireshark stream? Instead of analyzing each packet, one can see the direct data flow between the communication.
Now you need to do a trail and error process for each different packet you find.
```
right click on a specific packet --> choose follow --> the kind of stream available.
```
The flag resides in `udp.stream eq 6`

(or)

you can do the following if you're well experienced.
Known that there are only 4 types of streams given by default for wireshark/tshark, one can check manually.

```
$ PCAP=capture.pcap; END=$(tshark -r $PCAP -T fields -e udp.stream | sort -n | tail -1); for ((i=0;i<=END;i++)); do tshark -r $ PCAP -Y "udp.stream eq $i" -T fields -e data.text -o data.show_as_text:TRUE 2>/dev/null | tr -d '\n' | grep "picoCTF"; if [ $? -eq 0 ]; then echo "(Stream #$i)"; fi; done
picoCTF{StaT31355_636f6e6e}
(Stream #6)
picoCTF{N0t_a_fLag}
(Stream #7)
```

__Flag__

> picoCTF{StaT31355_636f6e6e}
