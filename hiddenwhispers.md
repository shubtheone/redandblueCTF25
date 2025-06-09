# Hidden Whispers - Steganography<br>

Here we are given a Data file. After performing few operatiosn like exiftool and analysing it with chatgpt i came to know that this file has few changes in it so we just need to revert it back. And so i did. <br>

```
printf '\x89PNG' | dd of=Data bs=1 seek=0 count=4 conv=notrunc
mv Data Data.png
```
<br>

After performing this command i checked the png and it had XXXX in its magic headers instead of IHDR so I just replaced XXXX to IHDR <br>
<br>`printf 'IHDR' | dd of=Data.png bs=1 seek=12 count=4 conv=notrunc` <br>

and so I got the flag:<br>

![Data](https://github.com/user-attachments/assets/e7ad2fe5-1f9c-4e61-973b-c63026f78806)
<br>
