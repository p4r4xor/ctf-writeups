# shark on wire 2

__Problem__

> We found this packet [capture](capture.pcap). Recover the flag that was pilfered from the network. You can also find the file in /problems/shark-on-wire-2_0_3e92bfbdb2f6d0e25b8d019453fdbf07.

__Hint__

> None.

__Solution__

Given a capture file, I tried to do the same strategy used in shark on wire 1. But no avail.
```bash
$ tshark -r capture.pcap | head
1   0.000000 fe80::20c:29ff:fef7:6ad → ff02::fb     MDNS 180 Standard query 0x0000 PTR _nfs._tcp.local, "QM" question PTR _ftp._tcp.local, "QM" question PTR _webdav._tcp.local, "QM" question PTR _webdavs._tcp.local, "QM" question PTR _sftp-ssh._tcp.local, "QM" question PTR _smb._tcp.local, "QM" question PTR _afpovertcp._tcp.local, "QM" question
    2   0.000494     10.0.0.6 → 224.0.0.251  MDNS 160 Standard query 0x0000 PTR _nfs._tcp.local, "QM" question PTR _ftp._tcp.local, "QM" question PTR _webdav._tcp.local, "QM" question PTR _webdavs._tcp.local, "QM" question PTR _sftp-ssh._tcp.local, "QM" question PTR _smb._tcp.local, "QM" question PTR _afpovertcp._tcp.local, "QM" question
    3  11.996569 fe80::5ca9:605:a9be:272d → ff02::fb     MDNS 180 Standard query 0x0000 PTR _ftp._tcp.local, "QM" question PTR _nfs._tcp.local, "QM" question PTR _afpovertcp._tcp.local, "QM" question PTR _smb._tcp.local, "QM" question PTR _sftp-ssh._tcp.local, "QM" question PTR _webdavs._tcp.local, "QM" question PTR _webdav._tcp.local, "QM" question
    4  11.996897     10.0.0.5 → 224.0.0.251  MDNS 160 Standard query 0x0000 PTR _ftp._tcp.local, "QM" question PTR _nfs._tcp.local, "QM" question PTR _afpovertcp._tcp.local, "QM" question PTR _smb._tcp.local, "QM" question PTR _sftp-ssh._tcp.local, "QM" question PTR _webdavs._tcp.local, "QM" question PTR _webdav._tcp.local, "QM" question
    5  16.004668 fe80::20c:29ff:fef7:6ad → ff02::fb     MDNS 180 Standard query 0x0000 PTR _nfs._tcp.local, "QM" question PTR _ftp._tcp.local, "QM" question PTR _webdav._tcp.local, "QM" question PTR _webdavs._tcp.local, "QM" question PTR _sftp-ssh._tcp.local, "QM" question PTR _smb._tcp.local, "QM" question PTR _afpovertcp._tcp.local, "QM" question
    6  16.005020     10.0.0.6 → 224.0.0.251  MDNS 160 Standard query 0x0000 PTR _nfs._tcp.local, "QM" question PTR _ftp._tcp.local, "QM" question PTR _webdav._tcp.local, "QM" question PTR _webdavs._tcp.local, "QM" question PTR _sftp-ssh._tcp.local, "QM" question PTR _smb._tcp.local, "QM" question PTR _afpovertcp._tcp.local, "QM" question
    7  23.397257  192.168.2.1 → 192.168.2.3  TCP 63 60218 → 80 [PSH, ACK] Seq=1 Ack=1 Win=2051 Len=9
    8  23.398075  192.168.2.3 → 192.168.2.1  TCP 60 80 → 60218 [PSH, ACK] Seq=1 Ack=10 Win=238 Len=3
    9  23.439183  192.168.2.1 → 192.168.2.3  TCP 60 60218 → 80 [ACK] Seq=10 Ack=4 Win=2051 Len=0
   10  29.557413 Vmware_b9:02:a9 → Broadcast    ARP 60 Who has 10.0.0.11? Tell 10.0.0.5
tshark: An error occurred while printing packets: Broken pipe.
```
We try to give the same bash script from shark on wire 1

```console
$ PCAP=capture.pcap; END=$(tshark -r $PCAP -T fields -e udp.stream | sort -n | tail -1); for ((i=0;i<=END;i++)); do tshark -r $PCAP -Y "udp.stream eq $i" -T fields -e data.text -o data.show_as_text:TRUE 2>/dev/null | tr -d '\n' | grep "picoCTF"; if [ $? -eq 0 ]; then echo "(Stream #$i)"; fi; done
picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!aaaaa
(Stream #9)
I really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flags
(Stream #10)

```
This time, I decided to check through all the UDP streams. 

```
$ PCAP=capture.pcap; END=$(tshark -r $PCAP -T fields -e udp.stream | sort -n | tail -1); for ((i=0;i<=END;i++)); do tshark -r $PCAP -Y "udp.stream eq $i" -T fields -e data.text -o data.show_as_text:TRUE 2>/dev/null | tr -d '\n'; echo ""; done






i6f6e
kfdsalkfsalkico{N0t_a_fLag}
icoCTF{StaT31355e
fjdbanlkfdnfjdbanlkfdnfjdbanlkfdnfjdbanlkfdnfjdbanlkfdnfjdbanlkfdnfjdbanlkfdnfjdbanlkfdnfjdbanlkfdn
picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!picoCTF Sure is fun!aaaaa
I really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flagsI really want to find some picoCTF flags

C
T
F
fjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdnfjdsakf;lankeflksanlkfdn


AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA


ffffffffffffffffffffffffffffffffffffffff

_
36
}
zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa




start
aaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaa
aaaaa
aaaaa
aaaaa
aaaaa
aaaaa
aaaaa
aaaaaaaaaa
aaaaaaaaaa
aaaaa
aaaaaaaaaaaaaaa
aaaaa
aaaaaaaaaa
aaaaaaaaaaaaaaa

aaaaaaaaaaaaaaa
bbb
aaaaaaaaaa

aaaaa
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
aaaaa
aaaaa
aaaaa
aaaaa
end
aaaaaaaaaa
aaaaa
aaaaaaaaaa
aaaaa
aaaaa


```

While I thought this was also some useless output, I caught with something that matters a lot.
There's something called start and end in the output.
Let us see what these actually mean.

```bash
$ tshark -nr capture.pcap  -Y 'frame contains "start"'
1104 991.587437    10.0.0.66 → 10.0.0.1     UDP 60 5000 → 22 Len=5
$ tshark -nr capture.pcap  -Y 'frame contains "end"'
1303 1171.059146    10.0.0.80 → 10.0.0.1     UDP 60 5000 → 22 Len=3
```
Nothing Interesting over here. All I could see is both go to the destination port 22.
Due to some luck, I've tried to dump all the packets going to port 22.

```
$ tshark -nr capture.pcap  -Y 'udp.dstport == 22'
1104 991.587437    10.0.0.66 → 10.0.0.1     UDP 60 5000 → 22 Len=5
 1106 993.672341    10.0.0.66 → 10.0.0.1     UDP 60 5112 → 22 Len=5
 1118 1006.227400    10.0.0.66 → 10.0.0.1     UDP 60 5105 → 22 Len=5
 1122 1008.323546    10.0.0.66 → 10.0.0.1     UDP 60 5099 → 22 Len=5
 1124 1010.428768    10.0.0.66 → 10.0.0.1     UDP 60 5111 → 22 Len=5
 1129 1012.535515    10.0.0.66 → 10.0.0.1     UDP 60 5067 → 22 Len=5
 1131 1014.627130    10.0.0.66 → 10.0.0.1     UDP 60 5084 → 22 Len=5
 1133 1016.719657    10.0.0.66 → 10.0.0.1     UDP 60 5070 → 22 Len=5
 1135 1018.807279    10.0.0.66 → 10.0.0.1     UDP 60 5123 → 22 Len=5
 1137 1020.899193    10.0.0.66 → 10.0.0.1     UDP 60 5112 → 22 Len=5
 1139 1022.991480    10.0.0.66 → 10.0.0.1     UDP 60 5049 → 22 Len=5
 1141 1025.083748    10.0.0.66 → 10.0.0.1     UDP 60 5076 → 22 Len=5
 1143 1027.167730    10.0.0.66 → 10.0.0.1     UDP 60 5076 → 22 Len=5
 1145 1029.255106    10.0.0.66 → 10.0.0.1     UDP 60 5102 → 22 Len=5
 1147 1031.334799    10.0.0.66 → 10.0.0.1     UDP 60 5051 → 22 Len=5
 1162 1043.850969    10.0.0.66 → 10.0.0.1     UDP 60 5114 → 22 Len=5
 1164 1045.934960    10.0.0.66 → 10.0.0.1     UDP 60 5051 → 22 Len=5
 1166 1048.019181    10.0.0.66 → 10.0.0.1     UDP 60 5100 → 22 Len=5
 1172 1054.255069    10.0.0.66 → 10.0.0.1     UDP 60 5095 → 22 Len=5
 1178 1060.507360    10.0.0.66 → 10.0.0.1     UDP 60 5100 → 22 Len=5
 1180 1062.619741    10.0.0.66 → 10.0.0.1     UDP 60 5097 → 22 Len=5
 1187 1066.779955    10.0.0.66 → 10.0.0.1     UDP 60 5116 → 22 Len=5
 1189 1068.867478    10.0.0.66 → 10.0.0.1     UDP 60 5097 → 22 Len=5
 1192 1070.959143    10.0.0.66 → 10.0.0.1     UDP 60 5095 → 22 Len=5
 1196 1073.043525    10.0.0.66 → 10.0.0.1     UDP 60 5118 → 22 Len=5
 1199 1075.127069    10.0.0.66 → 10.0.0.1     UDP 60 5049 → 22 Len=5
 1267 1139.786992    10.0.0.66 → 10.0.0.1     UDP 60 5097 → 22 Len=5
 1272 1141.870974    10.0.0.66 → 10.0.0.1     UDP 60 5095 → 22 Len=5
 1274 1143.955404    10.0.0.66 → 10.0.0.1     UDP 60 5115 → 22 Len=5
 1276 1146.043247    10.0.0.66 → 10.0.0.1     UDP 60 5116 → 22 Len=5
 1284 1154.383039    10.0.0.66 → 10.0.0.1     UDP 60 5051 → 22 Len=5
 1286 1156.475039    10.0.0.66 → 10.0.0.1     UDP 60 5103 → 22 Len=5
 1296 1166.882937    10.0.0.66 → 10.0.0.1     UDP 60 5048 → 22 Len=5
 1301 1168.975486    10.0.0.66 → 10.0.0.1     UDP 60 5125 → 22 Len=5
 1303 1171.059146    10.0.0.80 → 10.0.0.1     UDP 60 5000 → 22 Len=3
```
Was very happy on looking at this :) You can see that the source port were different everytime.
How different? Very different :)
The last three digits of each of the source port are different and the first port starts with `112` which is `p` in ASCII representation.
The following script now prints us the flag.

```python
from scapy.all import *

flag = ""

packets = rdpcap('capture.pcap')
for packet in packets:
    if UDP in packet and packet[UDP].dport == 22:
        flag += chr(packet[UDP].sport - 5000)
print flag
```

__Flag__

> picoCTF{p1LLf3r3d_data_v1a_st3g0}
