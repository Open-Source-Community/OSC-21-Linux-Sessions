# OSC linux Meeting - Forensics II - STEGANOGRAPHY.
##### Session Moderator: Ahmed Ayman.

## What is Steganography?

- Steganography is the practice of hiding data in plain sight. Steganography is often embedded in images or audio.

- Files are made of Bytes. _a Byte is 8 Bits_ _ a Bit contains either zero or one.

- Images are made of pixels, pixels are made of 4 bytes:

1. byte one is the alpha which changes controls the transparency of that exact pixel.
2. the next 3 bytes are R (Red) - G (Green) - B (Blue), which together decides
what is the color of this exact cell using the RGB color model.

## Steganagraphy Types 

### LSB Steganography

- LSB : Least Significant Bit. It's the right most bit in the byte which only changes the value of 2^0.
for example if you have a number 4 and you converted it to binary, then changed 
the LSB you will be adding 1 to 4. so it's not significant.

- This type of steganography uses the fact thet changing the lsb wouldn't make much differince in the image color.

> HOW? 
- how can you hide a string in an image using LSB Steganography? 
1. convert your message to binary.
2. get the image pixels.
3. change the LSB in each color byte (Ignoring the alpha byte) to your message binary bits.


### Secure Cover Selection Steganography

- This technique insated of changing the lsb of each pixel bytes, compares the blocks of the carrier 
image to the blocks of their message, if an image with the same blocks as the
message blocks is found, The identical message blocks are then carefully fitted into the carrier
image. The resulting image is identical to the original and the worst part is that 
this image is not flagged as a threat by detection software and applications.

### And many many others types

- Masking and filtering
- Redundant Pattern Encoding
- Encrypt and Scatter
- Algorithms and transformations


## TOOLS

### Steghide

> Instalation 
```bash 
sudo apt install steghide
```	
> Embed a file content into another file
```bash
steghide embed -ef <the secret file path> -cf <the file to hide the secret in path> -p <password to protect the data - could be null ->
```

> Extract embeded file from another file
```bash
steghide extract -sf <the embeded file> -p <password - could be null -> -xf <output file>
```

> Other options
```bash
man steghide
steghide --help
```

### Zsteg

- Detect stegano-hidden data in PNG & BMP.

> Instalation 
```bash 
sudo apt install gem
sudo gem install zsteg
```	

> Extract embeded file from another file
```bash
zsteg <image path> --algorithm 
# the algorithm is optional, the default will tryout all of them. 
```

> Other options
```bash
zsteg --help
```


### Stegcracker

- Steganography brute-force utility to uncover hidden data inside files

> Instalation 
```bash 
sudo apt install steghide
sudo apt install python3-pip #if pip not installed already
python3 -m pip install --user stegcracker
```	

> Usage
```bash
stegcracker <file> <wordlist> 
```

> Other options
```bash
stegcracker --help
```

### Binwalk

-  Binwalk is an open source firmware extraction tool that extracts embedded file systems from firmware images.

> Instalation 
```bash 
sudo apt install binwalk
```	

> Usage
```bash
binwalk -e <file> #extract 
```

> Other options
- there are too many options you can use.
```bash
man binwalk
binwalk -h
```
### There are tons of online steganography tools, you can find some of them in the resources file.

## Example Challenges:

> Reading Between the Eyes | Picoctf2018
> Problem: "Stego-Saurus hid a message for you in this image, can you retreive it?"
> Hints: "Maybe you can find an online decoder?"
1. download the image.
![husky.png](Challenge0/husky.png)
2. run file command.
```bash
file husky.png # husky.png: PNG image data, 2140 x 2232, 8-bit/color RGBA, non-interlaced
```	
3. it's PNG so let's tryout ZSTEG.
```bash
zsteg challenge0/husky.png
```
```
b1,r,lsb,xy         .. text: "^5>c[rvyzrf@"
b1,rgb,lsb,xy       .. text: "picoCTF{r34d1ng_b37w33n_7h3_by73s}"
b1,abgr,msb,xy      .. file: PGP\011Secret Sub-key -
b2,g,msb,xy         .. text: "ADTU@PEPA"
b3,abgr,msb,xy      .. text: "t@Wv!Wt\tGtA"
b4,r,msb,xy         .. text: "0Tt7F3Saf"
b4,g,msb,xy         .. text: "2g'uV `3"
b4,b,lsb,xy         .. text: "##3\"TC%\"2f"
b4,b,msb,xy         .. text: " uvb&b@f!"
b4,rgb,lsb,xy       .. text: "1C5\"RdWD"
b4,rgb,msb,xy       .. text: "T E2d##B#VuQ`"
b4,bgr,lsb,xy       .. text: "A%2RTdGG"
b4,bgr,msb,xy       .. text: "EPD%4\"c\"#CUVqa "
b4,rgba,lsb,xy      .. text: "?5/%/d_tO"
b4,abgr,msb,xy      .. text: "EO%O#/c/2/C_e_q"
```
4. we got the flag from the lsb algorithm.
-- aditional step to test zsteg
5. now that we now it's embeded using lsb algorithm we can use 
```bash
zsteg challenge0/husky.png --lsb
```
flag: picoCTF{r34d1ng_b37w33n_7h3_by73s}


