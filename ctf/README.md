# CTF

I've been playing lots of CTFs lately and there's lot to learn in them and some times the challenges are either repeated or are of similar type so it's better to keep a record of them. So I started making CTF notes.

## CTF Tools

Just some tools we use

### web

* Nikito:
  * [https://github.com/sullo/nikto](https://github.com/sullo/nikto)
* SQLmap
  * [https://github.com/sqlmapproject/sqlmap](https://github.com/sqlmapproject/sqlmap)

### Reversing

* Radare2
  * [https://github.com/radare/radare2](https://github.com/radare/radare2)
  * cutter:
    * GUI mode of radare2
    * [https://github.com/radareorg/cutter](https://github.com/radareorg/cutter)
* pwndbg
  * [https://github.com/pwndbg/pwndbg](https://github.com/pwndbg/pwndbg)
  * with
    * pedas: [https://github.com/longld/peda](https://github.com/longld/peda)
    * voltron: [https://github.com/snare/voltron](https://github.com/snare/voltron)
* checksec
  * [https://github.com/slimm609/checksec.sh](https://github.com/slimm609/checksec.sh)
    * Check if canary etc are enabled or not

### Crypto

* [https://quipqiup.com/](https://quipqiup.com/)
* caesar: [https://cryptii.com/pipes/caesar-cipher](https://cryptii.com/pipes/caesar-cipher)
* vignere: [https://www.guballa.de/vigenere-solver](https://www.guballa.de/vigenere-solver)
* rot: [https://www.dcode.fr/rot-cipher](https://www.dcode.fr/rot-cipher)
* Substituion: [https://www.guballa.de/substitution-solver](https://www.guballa.de/substitution-solver)
* [I.C calculator](http://practicalcryptography.com/cryptanalysis/text-characterisation/index-coincidence/)
  * Use this if you have no clue which type of cipher it is.
* General
  * [https://quipqiup.com/](https://quipqiup.com/)
* RSA:
  * [https://github.com/Ganapati/RsaCtfTool](https://github.com/Ganapati/RsaCtfTool)
  * [https://github.com/ius/rsatool](https://github.com/ius/rsatool)
  * [https://www.alpertron.com.ar/ECM.HTM](https://www.alpertron.com.ar/ECM.HTM)
    * Best for factorizing etc
  * Also some scripts written in python.
  * libnum
    * [https://github.com/hellman/libnum](https://github.com/hellman/libnum)
    * Python library
* md5 hash
  * [https://www.md5online.org](https://www.md5online.org)


### Misc

* For mathematics
  * Use sympy or sage
    * sympy: [https://github.com/sympy/sympy](https://github.com/sympy/sympy)
    * sage:
* John the ripper
  * [https://www.openwall.com/john/](https://www.openwall.com/john/)
  * [https://github.com/magnumripper/JohnTheRipper](https://github.com/magnumripper/JohnTheRipper)
* Metasploit framwork
  * [https://github.com/rapid7/metasploit-framework](https://github.com/rapid7/metasploit-framework)
* Git related task:
  * gittools: [https://github.com/internetwache/GitTools/](https://github.com/internetwache/GitTools/)
* vsftp
  * First thing to check is that if the given vsftp version isn't vulnerable to any kind of know vulnerability
    * Could be simple as: [https://ctftime.org/writeup/12060](https://ctftime.org/writeup/12060)
  * [https://en.wikipedia.org/wiki/Vsftpd](https://en.wikipedia.org/wiki/Vsftpd)
* [dirb](https://tools.kali.org/web-applications/dirb)
  * Look for all the accesible directories on a server
  * Not always useful but sometime a life saver
* hydra along with our lovely [`rockyou.txt`](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=2ahUKEwjF_6fRjIvfAhUJtI8KHeGqCGkQFjAAegQIBxAB&url=https%3A%2F%2Fgithub.com%2Fbrannondorsey%2Fnaive-hashcat%2Freleases%2Fdownload%2Fdata%2Frockyou.txt&usg=AOvVaw3snAERl1mU6Ccr4WFEazBd)

### Shell

* Ripgrep
  * [https://github.com/BurntSushi/ripgrep](https://github.com/BurntSushi/ripgrep)
* strings
* cat
* \|\(pipe\)

## Leaks

* [https://gitlab.com/glicOne/shadowbroker](https://gitlab.com/glicOne/shadowbroker)
* Hack scripts
  * [https://gitlab.com/glicOne/hack\_scripts](https://gitlab.com/glicOne/hack_scripts)
* books
  * [https://gitlab.com/glicOne/knowledge-base](https://gitlab.com/glicOne/knowledge-base)
  * [https://github.com/RomaniukVadim/knowledge-base](https://github.com/RomaniukVadim/knowledge-base)
* CTF wiki
  * [https://gitlab.com/glicOne/ctf-wiki](https://gitlab.com/glicOne/ctf-wiki)
* Terminator ?
  * [https://gitlab.com/glicOne/Terminator](https://gitlab.com/glicOne/Terminator)


## Other lists

There are already many great lists that would help you during CTF. Some good list to check out are:

* trailofbit's [CTF Guide](https://trailofbits.github.io/ctf/)
    - A very good guide to get an idea about CTFs and different type of challenges

* John Hammond's [CTF Katana](https://github.com/JohnHammond/ctf-katana)
    - Really good and short notes.
    - He keeps track of all the `not so common` challenges from CTFs

* [CTF Candy](https://github.com/flawwan/CTF-Candy)
    - Good notes on web challenges

* [Security tips](https://github.com/Anonyme1396/security-tips)
    - Very good notes on WEB and RE/PWN category

* [CTF Wiki](https://gitlab.com/glicOne/ctf-wiki)
    - Good notes on WEB and CRYPTO

* [Knowledge base](https://gitlab.com/glicOne/knowledge-base)
