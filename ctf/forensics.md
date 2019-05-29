# Forensics

Forensics is a really good field but can be very frustrating sometimes. These are the things I have learned till now about this field.

Everything that I've learned in the field of `Forensics` is from __@UnblvR__
His knowledge in this field is God level and mostly I solve this category of challenges with him.

## Initiation

These are the some tools/command you should always start with or atleast test for forensics challenge

### Checking the `strings` in that image

```text
>>> strings <file_name>
```

strings is a Linux command that gives you all the string present in the image. Most of the time you'll find the flag here in normal or base64 format. To make your work easy you can use it with `grep`

```text
    >>> strings <file_name> | grep -i <string_to_be_searched>
```

```text
The `-i` flag is for `ignoring the case(lower/upper)`
```

### Check the Metadata

Always check the metadata of the file you are given\(unless the file is of unknown type\). [Exiftool](https://github.com/exiftool) is basically the best tool for this job. Metadata can give you lots of things like maybe there's an `author note` or `comment` or base64 strings. Sometimes images/files can have location headers in metadata, so say you are asked to find the location of some bogus HQ, start with metadata and see if there are any longitude or latitude header in there if yes then that might be the location which you are looking for.

Things might not be that easy always but it's really helpful to check the metadata.

## Extraction

Most of the time forensics challenges involve extracting files from an image or random data files. So here are the tricks/tools you can use to do so

#### [Binwalk](https://github.com/ReFirmLabs/binwalk) or [foremost](https://github.com/korczis/foremost)

Both of these tools are almost the same and they are used to extract hidden files\(if any\) in the image or any other file.

```text
>>> binwalk -e <filename>
>>> foremost -i <filename>
```

You can use any of those commands and you'll get all the files that could be extracted.

If you are using binwalk then you'll notice that binwalk almost every time gives you some `.zlib` file which actually isn't useful most of the time but you still wanna `grep` that file with `flag` format

```text
grep -i flag *
```

You can run that command in the recovered files directory just to be sure.

#### [Steghide](https://github.com/StefanoDeVuono/steghide)

I don't use this tool very often but sometimes the challenge is purely focused on this tool so I use it for simple extraction of a file. Sometimes using binwalk/foremost won't extract any file even if it's there because those files aren't hidden in a normal way. Steghide takes passphrase to extract the file, so if any challenge mention something about the passphrase or it hint's you in a way that steghide is involved then you'll need the passphrase.

```text
 steghide extract -sf fixed.bmp
```

With the command mentioned above, you can extract files hidden inside.

**Where to find the PassPhrase?**

Well this can vary from the difficulty of the challenge like if it's an easy challenge then there will be some hint provided in the problem statement itself, say the you are given an image of guys sitting with laptops and the hint says `what are they?` then you can guess with words like `geeks`, `hackers` and stuff.

Other than that the passphrase could be present in the metadata of that file. For that, you might wanna use `exiftool` and check for something different maybe `author's note` or `comment` or maybe a base64 string present.

Also if the challenge is difficult then surely there would be other hints/statement provide. Sometimes there are challenges that have to be brute forced in that case you can use scripts like [steg\_brute](https://github.com/Va5c0/Steghide-Brute-Force-Tool/blob/master/steg_brute.py) or [stegcracker](https://github.com/Paradoxis/StegCracker/blob/master/stegcracker) or simple code like

```bash
for passphrase in $(cat $2); do
  response=$(steghide extract -sf $1 -p "$passphrase" 2>&1);
  if [[ ! $response == *"could not extract"* ]]; then
    printf "%s\n\n" "$response";
    exit
  fi
done
```

**NOTE** There is rarely any challenge that will ask you to brute force steghide, so instead of direct brute-forcing, it tries to figure out the password from whatever you are given.

#### [StegoVeritas](https://github.com/bannsec/stegoVeritas/)

I recently came to know about this tool\(thanks to **UnblvR**\) and started using this, mostly for [LSB](https://en.wikipedia.org/wiki/Bit_numbering#Least_significant_bit) extraction and some time for normal file extraction. There can be a challenge which might be hiding stuff in LSB so you can simply use this script like

```bash
python stegoVeritas <filename>
```

This will generate a lot of images with all the different pixels in different shades and stuff. Also, it makes a folder name `result` which sometimes contains any kind of hidden file.

#### [Zsteg](https://github.com/zed-0xff/zsteg)

I don't use this tool anymore but this tool is worth a try. The problem with this tool is that it doesn't support jpeg and different type of extensions\(only supports PNG\). I used this tool for a while but now for LSB and stuff you can use StegoVeritas.

# Audio analysis

This is a category of forensics challenges are the weird ones or at least that's how I feel :smile:

For most of the audio file, you can use [audacity](https://www.audacityteam.org/) or [Sonic Visualiser](https://www.sonicvisualiser.org/).

Now there isn't anything fixed but most of the time challenge creator puts the flag in the [spectrogram](https://en.wikipedia.org/wiki/Spectrogram) and for that, I have found Sonic visualizer more helpful then audacity, but that's just a personal preference you can get that in both\(audacity or sonic\). Just get the Spectogram and try to change the color or width of the spectrogram.

In many audio files, there would be some high pitch, in that case, you can try the [audio morse decoder](https://morsecode.scphillips.com/labs/decoder/). Just upload the file and try to change the speed\(only if you are sure that it's a morse code\).

# Data/Broken files

Now, this is the most difficult category of challenges. They are difficult because they are totally vague.

**What kind of challenges are involved in this?**

Well a file will be provided and if you try to check the type using file command you'll nothing like

```bash
file <filename>
>>> file: data
```

As you can see the file command doesn't show anything. Also, you won't be able to open the file in anything like when you double click the file system will ask you with which application you'll like to open the file.

**How to tackle them?**

Well, this is not as easy as using binwalk or string. I am also currently in the process of learning but I'll share what I know.

1\) It could be as easy as using binwalk on it :smile:

Sometime someone might have just hidden the stuff and that "stuff" could be extracted using binwalk or foremost or any other extraction tool. In that case, it would totally depend on what you get after extraction.

2\) When the headers are messed up

As I said in the starting that even the `file` command may also fail, that's because file command looks for specific headers in the starting of the file and if those are recognized it reports the file type.

**NOTE** `file` command doesn't only looks for the header it also finds some other magic number at specific positions. You can read more: [https://en.wikipedia.org/wiki/File\_\(command](https://en.wikipedia.org/wiki/File_%28command)\)

Now, this type can vary from very easy to difficult.

The easy ones could be checking the header with [`xxd`](http://www.tutorialspoint.com/unix_commands/xxd.htm) or [`hexyl`](https://github.com/sharkdp/hexyl) to find the header

```bash
>>> xxd -l8 <filename>
```

or

```bash
>>> hexyl -n8 <filename>
```

In both of the command, the number `8` gives the first 8 octets bytes of the file\(the headers\). If the headers are messed up you can look for similar kind of headers of [wikipedia](https://en.wikipedia.org/wiki/List_of_file_signatures) or [filesignature.net](https://www.filesignatures.net/) and try fixing it.

**Example:**

Say we are given an image called `hack.png` using xxd

```bash
>>> xxd -l8 hack.png
45 65 4E 47 0D 0A 1A 0A
```

These aren't any valid headers but if you replace the `45` with `89` and replace the `65` with `50` i.e the headers become

```text
89 50 4E 47 0D 0A 1A 0A
```

That would make it a valid PNG file and then you can see what's in it.

This same challenge could be made difficult by keeping the headers of a valid file and the other remaining content/data of different file type which can confuse you.

**Example:**

We are given a file which is of say `.PNG` extension. Using `file` command on it confirms that it's PNG but when we try to open the file in any viewer we can't see anything or the viewer gives an error like `Cannot open the file` etc That can be very confusing.

The real game could be that creator of the challenge took a ZIP file and replaced the header of that ZIP file with the headers of PNG so tools are reporting it as PNG. But the problem with these kinds of challenges is that they are totally based on how much experience you have with file and stuff. Because to solve these kinds of challenge you'll have to open the file in a hex editor\(I use [okteta](https://www.kde.org/applications/utilities/okteta/) on arch\) and then try to recognize the file with the other bytes in the file. Then figure out which byte is messed up and fix that one.

# Memory forensics

I just love these kinds of challenges, even though I am very bad at them but I really enjoy working on them.

**What type of challenges are included in this category?**

Basically you are provided with a memory dump of a hard drive and then you have to answer questions based on them.

I first came across this type of challenges in OtterCTF 2018 \(read my [writeups](https://github.com/mzfr/ctf-writeups/tree/master/OtterCTF%202018/Memory%20Forensics)\).

**How to tackle them?**

[Volatility](https://github.com/volatilityfoundation/volatility) is your answer. It's a collection of a tool which basically helps you figure stuff out.

You can refer to the following resources for volatility usage:

1\) [PDF](https://downloads.volatilityfoundation.org/releases/2.4/CheatSheet_v2.4.pdf)

2\) [SANS Cheatsheet](https://digital-forensics.sans.org/media/volatility-memory-forensics-cheat-sheet.pdf)

3\) [Command reference](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference)

4\) [aldeid examples](https://www.aldeid.com/wiki/Volatility)

**Most common type of questions that are asked :=**

**1\)** hostname and computer name of the user

For hostname - Read [https://www.aldeid.com/wiki/Volatility/Retrieve-hostname](https://www.aldeid.com/wiki/Volatility/Retrieve-hostname) For Password - Read [https://www.aldeid.com/wiki/Volatility/Retrieve-password](https://www.aldeid.com/wiki/Volatility/Retrieve-password)

You can also use [mimkatz](https://raw.githubusercontent.com/dfirfpi/hotoloti/master/volatility/mimikatz.py)

```bash
volatility  — plugins=<path-to-mimkatz-file> — profile=<profile-name> -f <memory dump> mimikatz
```

Sometime mimikatz doesn't give any output in that case you can just follow the first method.

**2\)** Find the IP and port for computer:

    Just run the netscan command and go through the output.

**3\)** Find the content clipboard

    Again use the simple `clipboard` command to get the content of the clipboard.

**4\)** Finding out the malware

    This is the real reason these kinds of challenges are made.
    In real life scenario, people take memory dumps just to analyze for malware.

Finding malware could be confusing if you don't know what files stays in what place and what they do. For that kind of information, you can read:

1\) [https://www.sans.org/security-resources/posters/dfir-find-evil/35/download](https://www.sans.org/security-resources/posters/dfir-find-evil/35/download)

2\) [https://www.sans.org/security-resources/posters/windows-forensics-evidence-of/75/download](https://www.sans.org/security-resources/posters/windows-forensics-evidence-of/75/download)

Basically, you have to go through the `pstree` and see which process is the child to some weird parent process. Say there is a process named `iexplorer.exe` running but it has a child process named `cmd.exe` which is weird because if you think about it why would `iexplorer` run `cmd` for anything. So then you can start looking deeply into those process.

Also sometime you might have to extract out those files and try to run those malware\(please do that in VM :wink:\)

***

Another type memory forensics challenge I came across was in one CTF where we were given the memory dump along with a `.dwarf` & `system.map` file.
If you see these files provided with the memory dump then it's the profile for that memory dump.
Basically if you run `volatility` on that memory dump it won't be able to suggest the `profile` of that dump. That is where those other two files come in handy.

Step to use those files:

1) Zip `.dwarf` and `system.map` file together.
2) Put that zip file in a folder
3) Pass that folder to the `--plugin` argument in volatility.

Ex:

`vol.py --plugins=/path/to/zip/containing/folder -f <memdump name>  imageinfo`

**Note** - It's important that you keep the zip file into a folder and pass that folder to the plugin argument

Nothing much can be said about this field because things are pretty fixed like you know the command are known and all it needs is patience to figure out stuff.

## PCAP files

These ones are again some pretty vague and there isn't anything fixed here. Basically, you are provided with a PCAP file and that would have what you are looking for. Best way to analyze them is [Wireshark](https://www.wireshark.org/). After opening you can see the protocols, if there are any HTTP or SMTP type then best is to export all the objects that could be exported and try looking into them. If it has some weird\(not very common\) protocol then it's just best to try analyzing the requests and find some pattern.

Sometime you'll have to trim all the PDUs with some specific size to actually get the correct PCAP sometime you'll have to see hidden stuff in the Stream.

Also you might be asked question like `Ip of the attacker` or `Ip of the host` or `Which port was open` etc for these kind of things you can use tshark like

```text
➜ tshark -r capture.pcap -z conv,tcp -q
```

This will give you a list of ports along with IP.

You can also use [scapy](https://scapy.net/) to grab some data that might not be clear with wireshark or couldn't be extracted using wireshark. For example protocols like `ICMP`.

Another great tool for PCAP is [ngrep](https://github.com/jpr5/ngrep)

# File System

These kind of challenges involve `.img` or similar files from which you are expected to extract content or deleted files and do the stuff. Most of these challenges are pretty straight forward\(unless bytes of those files are messed up\).

You can use [`testdisk`](https://www.cgsecurity.org/wiki/TestDisk) or [`photorec`](https://www.cgsecurity.org/wiki/PhotoRec). These tools extracts most of the files so you don't have to mount the image etc.But sometime\(when size is large\) you should mount the file and then analyse everything. Start looking from the `/home` and then follow the trail.

You can then focus on logs like `auth.log` that will tell you who has logged in and on what time. That can be then used to find files after that period of time.

```text
➜ find . -type f -newermt "Feb 17 00:06:04"
```

The above command find all the files that were changed on 17 Feb at 00:06:04

This is just the example, but point to keep in mind is that if the filesystem in big in size just mount it.

Sometime you might end up having an ecrypted file system which you have to decrypt first using a password. Now if some other info is given about the password use that but if you are expected to bruteforce that password then the best and maybe the only possible way is to dump the header of that file which will contain the hashes of the password and then use that dump with hashcat to crack it.

You can use `dd` command to dump the headers\(you need offset for that\).

## Tools

Some other tools that can be used are:

1\) [https://29a.ch/photo-forensics/\#forensic-magnifier](https://29a.ch/photo-forensics/#forensic-magnifier)

This can be used in the type of challenges in which an image is made of multiple layers and you have to look into that. Ex: \[PicoCTF's Now you don't\]\([https://github.com/mzfr/ctf-writeups/tree/master/picoCTF-2018/Forensics/now you don't ](https://github.com/mzfr/ctf-writeups/tree/master/picoCTF-2018/Forensics/now%20you%20don't%20)\)

2\) [SleuthKit](https://www.sleuthkit.org/sleuthkit/)

This is a very powerful tool but you must have some knowledge about file stuff like bytes etc.

3\) [crontab expression decoder](https://crontab.guru/)

Basically there are some stars `*` and stuff in crontab file so that could be changed using this.

