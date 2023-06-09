`Description`
Challenge Author: clides
Being the APT (advanced persistent troll) he is, clides continued to play around with Claudio Pacheco's laptop without him knowing. He even gained access to Claudio's friend's device. On that device, he found this strange looking file and he wants to know what it contains.
Can you help clides retrieve hidden info from this file?
foren3.zip

`Writeup by: RJCyber`
Taking a look at the file contained in foren3.zip, we can see there is a broken BMP file.
![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/893d21c8-dd7e-4dab-bed4-fcf571d9c21f)

Let's take a deeper dive into the BMP file format.
Source: https://en.wikipedia.org/wiki/BMP_file_format
Taking a look at the wikipedia article, we can see that the "magic bytes" (42 4D in this case) are correct! Well, why is the image still broken??!! It's because of the broken BMP header as well as the DIB header.

![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/cdf680c0-dfca-4a77-b355-472eab034b09)

That's odd, why does it have DE AD? Let's fix this using the article we found earlier.

![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/9d625a5a-733f-4c68-ba16-f8e1944a9a69)

According to this, we can replace the first DE AD with 00 00 because they are unused bytes.
![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/48451887-7f19-4922-ba7e-912827b45a0a)

Additionally, we can replace the second DE AD with the first part of the DIB header:
![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/5951c4e6-af14-4134-bfdc-b4656aac160e)
So, let's replace the second DE AD with 28 00.

Now, we have a recovered BMP image!
![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/60859026-229d-4eeb-ba15-7da4bc32e0d9)
YAY, we got our flag! `ctf{totally_the_correct_flag}`

BUT WAIT, THERE'S MORE! Hey, that flag doesn't work ._.

Let's take an even deeper look. Hmm, the margins look a bit sus. Where in the world is the top margin?!

Let's go back to the article.
![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/e2de179c-1cf9-49c9-84f3-71b4b42af157)
Hmm, this looks interesting. So, the 8th byte after the DIB header governs the height of the image. 
![image](https://github.com/OfficialCyberSpace/CTF-Writeups/assets/86359182/f0b39007-ac65-4956-9a17-95f675ed0a61)

Let's try to change the height.
...
Now, let's try to see if it gives us the flag.


