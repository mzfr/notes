# CTF Tools

Just some tools we use

## web

+ Nikito:
    - https://github.com/sullo/nikto
+ SQLmap
    - https://github.com/sqlmapproject/sqlmap

## Reversing

+ Radare2
    - https://github.com/radare/radare2
    - cutter:
        * GUI mode of radare2
        * https://github.com/radareorg/cutter

+ pwndbg
    - https://github.com/pwndbg/pwndbg
    - with
        *  pedas: https://github.com/longld/peda
        *  voltron: https://github.com/snare/voltron

+ checksec
    - https://github.com/slimm609/checksec.sh
        + Check if canary etc are enabled or not

## Crypto

- https://quipqiup.com/
- caesar: https://cryptii.com/pipes/caesar-cipher
- vignere: https://www.guballa.de/vigenere-solver
- rot: https://www.dcode.fr/rot-cipher
- Substituion: https://www.guballa.de/substitution-solver
- [I.C calculator](http://practicalcryptography.com/cryptanalysis/text-characterisation/index-coincidence/)
    + Use this if you have no clue which type of cipher it is.

- General
    + https://quipqiup.com/

- RSA:
    + https://github.com/Ganapati/RsaCtfTool
    + https://github.com/ius/rsatool
    + https://www.alpertron.com.ar/ECM.HTM
        * Best for factorizing etc

    + Also some scripts written in python.
    + libnum
        * https://github.com/hellman/libnum
        * Python library
- md5 hash
    + https://www.md5online.org

## Forensics:

+ tesdisk
    - https://www.cgsecurity.org/wiki/TestDisk
+ Sleuthkit
    - https://www.sleuthkit.org/sleuthkit/
    - https://www.sleuthkit.org/sleuthkit/framework.php
    - man: http://www.sleuthkit.org/sleuthkit/man/

+ Wireshark
    - https://www.wireshark.org/
    - Also use tshark to play with pcaps in terminal
    - If it's web traffic, then start with POST requests

+ zsteg
    - https://github.com/zed-0xff/zsteg

+ Images:
    - https://29a.ch/photo-forensics/#forensic-magnifier
    - http://stylesuxx.github.io/steganography/
+ Text Files
    - dos2unix
        + If the file contain `CRLF line terminators`

+  If given text looks like shit and you have no clue what it is then check for any [esoteric language](https://en.wikipedia.org/wiki/Esoteric_programming_language)
    - [linguist](https://github.com/github/linguist)

+ For PGP
    - https://sela.io/pgp/
    - If PGP message or anything related PGP is given then there has to be something else given to the PGP like passphrase, PGP private key soemthing else.
    - Mostly the passphrase are something from the question.

+ Broken images/zips
    - One thing to try is to test for the signature of the files.
        * https://en.wikipedia.org/wiki/List_of_file_signatures
    - Try: `https://github.com/TheZ3ro/zipfix`

+ Audio files
    - Sonic visualize: https://www.sonicvisualiser.org/
    - Audacity: https://www.audacityteam.org/
    - Check spectrogram first for any given audio file and don't forget to change colors of spectrogram.

+ https://www.monkey.org/~dugsong/dsniff/

## Malware analysis

+ Volatility
+ https://www.hybrid-analysis.com/
    * Upload file and perform malware analysis
+ https://digital-forensics.sans.org/media/SANS_Poster_2018_Hunt_Evil_FINAL.pdf
    * Some informations about the files present in windows mem dump

## Misc

* For mathematics
    + Use sympy or sage
        - sympy: https://github.com/sympy/sympy
        - sage:

* John the ripper
    + https://www.openwall.com/john/
    + https://github.com/magnumripper/JohnTheRipper

* Metasploit framwork
    + https://github.com/rapid7/metasploit-framework

* Git related task:
    + gittools: https://github.com/internetwache/GitTools/

* vsftp
    + First thing to check is that if the given vsftp version isn't vulnerable to any kind of know vulnerability
        - Could be simple as: https://ctftime.org/writeup/12060
    + https://en.wikipedia.org/wiki/Vsftpd

* [dirb](https://tools.kali.org/web-applications/dirb)
    - Look for all the accesible directories on a server
    - Not always useful but sometime a life saver

* hydra along with our lovely [`rockyou.txt`](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=2ahUKEwjF_6fRjIvfAhUJtI8KHeGqCGkQFjAAegQIBxAB&url=https%3A%2F%2Fgithub.com%2Fbrannondorsey%2Fnaive-hashcat%2Freleases%2Fdownload%2Fdata%2Frockyou.txt&usg=AOvVaw3snAERl1mU6Ccr4WFEazBd)

## Shell

* Ripgrep
    - https://github.com/BurntSushi/ripgrep
* strings
* cat
* |(pipe)


# Leaks
+ https://gitlab.com/glicOne/shadowbroker

+ Hack scripts
    * https://gitlab.com/glicOne/hack_scripts
+ books
    * https://gitlab.com/glicOne/knowledge-base
    * https://github.com/RomaniukVadim/knowledge-base
+ CTF wiki
    * https://gitlab.com/glicOne/ctf-wiki
+ Terminator ?
    * https://gitlab.com/glicOne/Terminator
