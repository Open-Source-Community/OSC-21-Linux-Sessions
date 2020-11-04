# OSC linux Meeting - Foresnics I - FILE FORMATS AND META DATA
##### Session Moderator: [Youssef Fakhry](https://github.com/yeimsf)

## What is Digital Forensics?

- In Criminal Forensics there's an expert who lifts fingerprints and trails to analyze and figure out what actually happened in the crime scene, Digital Forensics is the digital version of this.

- It's the art of collecting and analyzing data in order to aquire certain details and trails guiding the Experts to understanding what actually happened in the crime scene.

- By understanding the scene, comes the correcting of the system, patching the vulnrabilities and restricting the access more than before allowing no such attack to happen again.

### File Formats:-

1. What are file extensions?

 ... File extensions are what tell us what kind of file this is.

 ... i.e [jpg, png, txt, zip, exe], specifying whether this file is an image, an archive, an executbale, etc.

2. How does the system know this file type?

... Every file has a format which tells the system how to interpret the data included in it.

... Through File Signatures aka. (File Magic Numbers), they are a specific sequence of hexadecimal characters being unique for each type of file,

... Ex: [JPEG. FF D8 FF E0 00 10 4A 46 49 46 00 01 , PNG. 89 50 4E 47 0D 0A 1A 0A , EXE. 4D 5A , etc..]

3. How to identify and display them?

... There are tools that can be used to identify them such as [hexdump, hexeditor, file].

4. Why do we look into them?

... There are several cases that the attacker will corrupt visible data in order to hide secret data or details on his fingerprints, as Digital Forensics Experts we use these tools to identify the type of corrupted file to try and extract these secret data the attacker is trying to hide.

#### Hex Dump

- A tool that can be used to extract hexadecimal format of the data the file is consisted of along with ASCII represntation of each hexadecimal byte.

> Installation **Although in most cases it's already installed on most distributions**
```bash
sudo apt install bsdmainutils
```

> Usage
```bash
man hd
hd __or__ hexdump [Option] <file-path> 
```
> Extracting Hex Dump Of File
```bash
hd __or__ hexdump -Cv <file-path>
# there are several options for use consult the man pages
```

#### Hex Editor

- A tool that can be used to extract and modify the hexadecmial contents of the file including the file signature associated with the file.
- This tool opens a GUI allowing for navigation and easy choosing of the file.

> Installation
```bash
sudo apt install ncurses-hexedit
```

> Usage
```bash
man hexeditor
hexeditor --help
hexeditor [Options]
# hexeditor can be used with no options as it opens a GUI to choose the file intended for editing
```

#### File

- A tool used to automatically identify the file signature and display the type of file.


> Installation **Although in most cases it's already installed on most distributions**
```bash
sudo apt install file
```

> Usage
```bash
man file
file [Option] <file-path>
```


#### There Are Loads Of Other Hex Editors And Tools For Identifying File Contents And Type


### Meta Data

1. What are Meta Data?

... Meta Data are data that describes other data and they are embedded in files containing addtional information and description.

2. What kind of data?

- An Image for example can contain headers like:-

..* Resolution of the image
..* Location of where the image was taken

> There are more of meta data headers than can be integrated in files, along with custom headers.

3. How to display them?

... The most popular tool used is Exiftool.

4. Why do we look into?

... as stated earlier, they can contain the location of where the image was taken, custom headers can also contain sensitive information, software/hardware used to make the file, time of creation and time of editing, etc..

#### Exiftool 

- A tool used to extract meta data of a file


> Installation
```bash
sudo apt install exiftool
```

> Usage
```bash
man exiftool
# exiftool documentation is found on their website [Exiftool Documentation](https://exiftool.org/exiftool_pod.html)
exiftool [Option] <file-path>
```

### Example Challenges:

> 1: I love images | Cybertalents
> Problem: "A hacker left us something that allows us to track him in this image, can you find it?"

1. Download The Image.
![godot.png](Challenge1/godot.png)

2. Run file command.
```bash
file godot.png # godot.png: PNG image data, 64 x 64, 8-bit/color RGBA, non-interlaced
# The file has been proven to be a png not a corrupt file
```
3. We can check for data within the hexadecimal content of the file by the hexdump command.
```bash
hexdump -Cv godot.png | head
```
```
00000000  89 50 4e 47 0d 0a 1a 0a  00 00 00 0d 49 48 44 52  |.PNG........IHDR|
00000010  00 00 00 40 00 00 00 40  08 06 00 00 00 aa 69 71  |...@...@......iq|
00000020  de 00 00 0d 71 49 44 41  54 78 9c e5 9b 7b 70 54  |....qIDATx...{pT|
00000030  55 9a c0 7f e7 de 7e a6  f3 ea 0e 49 e7 41 02 09  |U.....~....I.A..|
00000040  24 01 32 24 80 48 00 45  2c 20 0a 28 e0 b0 3e c0  |$.2$.H.E, .(..>.|
00000050  b1 d8 99 01 5c 76 76 71  74 77 6a c6 d9 81 9a 7d  |....\vvqtwj....}|
00000060  d4 c0 48 a9 53 e5 cc a8  e5 2a a8 a0 e8 c2 30 0b  |..H.S....*....0.|
00000070  b8 88 0a 8e c3 53 5e f2  0a 42 08 21 24 90 84 74  |.....S^..B.!$..t|
00000080  a0 f3 e8 f7 f3 ee 1f 21  91 90 4e a7 9b 74 04 c6  |.......!..N..t..|
00000090  5f 55 aa 6e ee 39 e7 3b  df f7 dd d3 e7 f1 9d 73  |_U.n.9.;.......s|

# Clearly the file says its png given the png file signature is present translated into PNG ascii representation on the right side 
```
4. We can check for the last content by hexdump command
```bash
hexdump -Cv godot.png | tail
```
```
00000d50  77 e1 f2 b4 cb b3 da d9  6c 59 da f4 75 fb e5 e9  |w.......lY..u...|
00000d60  4e 43 1d 57 6a 03 5e 9f  7f ab 2e 25 65 8b 97 80  |NC.Wj.^....%e...|
00000d70  4f 2d 54 26 a1 28 3a 84  b8 73 8e 87 85 a2 fd fa  |O-T&.(:..s......|
00000d80  7c 8d 33 e8 79 3f 10 f4  ff 63 e3 d9 93 ff dd 5a  ||.3.y?...c.....Z|
00000d90  7d b4 73 ee fc ff ea d0  4a 7e 75 fa 71 4b 00 00  |}.s.....J~u.qK..|
00000da0  00 00 49 45 4e 44 ae 42  60 82 49 5a 47 45 43 52  |..IEND.B`.IZGECR|
00000db0  33 33 4a 5a 58 58 49 58  32 50 4e 5a 57 48 53 58  |33JZXXIX2PNZWHSX|
00000dc0  32 43 4d 46 5a 57 4b 4e  52 55 50 55 3d 3d 3d 3d  |2CMFZWKNRUPU====|
00000dd0  3d 3d 0a                                          |==.|
00000dd3
# our flag is present here in a base32 encoding by copying it and decoding it with a built in command base32
```
- We also could've extracted the base32 string using the command strings
```bash
strings godot.png | tail
```
```
%rG'
*TYlT_qP
vL.I
VMqa.%
pDuF(
op+P
q}'ZA0
O-T&
IEND
IZGECR33JZXXIX2PNZWHSX2CMFZWKNRUPU======
```

5. We acquired the flag but encoded in base32, we have to decode it using base32 command
```bash
echo "IZGECR33JZXXIX2PNZWHSX2CMFZWKNRUPU======" | base32 -d
```
flag: FLAG{Not_Only_Base64}


> 2: Hidden Message | Cybertalents
> problem: "A cyber Criminal is hiding information in the below file . capture the flag ? submit Flag in MD5 Format"
1. Download The Image
![hidden_message.jpg](Challenge0/hidden_message.jpg)

2. Run file command
```bash
file hidden_message.jpg # hidden_message.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 96x96, segment length 16, Exif Standard: [TIFF image data, big-endian, direntries=5], baseline, precision 8, 768x432, frames 3
# Clearly it's a JPEG file
```

3. We can check for meta data if there exists a hidden text in it
```bash
exiftool hidden_message.jpg
```
```
ExifTool Version Number         : 10.80
File Name                       : hidden_message.jpg
Directory                       : .
File Size                       : 72 kB
File Modification Date/Time     : 2020:10:21 17:29:30+02:00
File Access Date/Time           : 2020:11:03 21:56:35+02:00
File Inode Change Date/Time     : 2020:10:21 17:29:30+02:00
File Permissions                : rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 96
Y Resolution                    : 96
Exif Byte Order                 : Big-endian (Motorola, MM)
Current IPTC Digest             : c51d5b8d73a91167e7fe4bbe5b41e2c9
Envelope Record Version         : 2
Coded Character Set             : UTF8
Application Record Version      : 2
Copyright Notice                : b1a1f2855d2428930e0c9c4ce10500d5
Image Width                     : 768
Image Height                    : 432
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 768x432
Megapixels                      : 0.332
```

4. We can clearly see there are 2 headers one "Current IPTC Digest" and one "Copyright Notice".

... the problem stated that the flag will be visible in the form of md5 hash which is created and not translated meaning it only goes one way not like encodings, we can check in an online hash database if this hash is present in their databases but there was no luck so submitting both md5 is the only way, the first was wrong submission but the second turned out to be the flag.

flag: b1a1f2855d2428930e0c9c4ce10500d5


