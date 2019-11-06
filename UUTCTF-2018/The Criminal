# UUTCTF
WriteUps For The CTF

## The Criminal

As the hint suggests, the password we need to find is an uppercase one which we need to change it to a lowercase.
The common idea is from the given packets, we either think of it as:
1) Admin, Password setup for a website
2) Some Password to a file from the extracted pcap given the file is large (not always true)

So, We now first analyze the pcap file
Does contain a variety of protocols, so I decided to analyze each protocol individually.
As the hint suggested for a password, I started looking in the http section as they are the ones which contain the passwords.

I did found one but it doesn't lead us anywhere.

![Screenshot from 2019-04-25 23-10-55](https://user-images.githubusercontent.com/49688892/56869423-2b540300-6a1e-11e9-8b80-e8fd0ff5d386.png)

I now decide to export the packet bytes of http protocol from the following pcap file.

To do the following, File -> Export Packet Bytes/ Export Objects (HTTP)

The next thing I see is (Export Objects)

![export_packets](https://user-images.githubusercontent.com/49688892/56869328-08751f00-6a1d-11e9-994e-f1a3f4edaf69.png)

We see a 7z file named fl4g.7z and a png file named secret_password-1024x64.png
I decided to extract all of the files incase if it was a decoy.
Analyzed all the files and found nothing interesting except these two.

Opening the secret password png, we see the following text.

![secret_password-1024x64](https://user-images.githubusercontent.com/49688892/56869576-f648b000-6a1f-11e9-9d1e-0fe3f7b1f465.png)

Password : this_is_th3_s3cr3t_passw0rd_for_flag (It was a mistake from them to show both 0 and o as the same way)

Give this password to the 7z file and voila!

![Screenshot from 2019-04-29 01-51-35](https://user-images.githubusercontent.com/49688892/56869723-b8e52200-6a21-11e9-88e6-35f0806ad140.png)

Flag: UUTCTF{d0_n0t_sav3_pa$$word_in_public}
