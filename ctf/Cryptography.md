# Cryptography

This is kinda weird category because either this will contain very simple challenges like decoding bases, solvig ciphers like caesar, subsititution or this will have challenges that will require a very good understanding for Mathematics.


## Basic Ciphers

These type of challenges can contain very basic ciphers to be decoded using online tools. Like decode the given caesar cipher or the vignere cipher etc

All this can be done by using simple online tools.

My goto tools are:

* For caesar cipher
    - [caesar-cipher](https://cryptii.com/pipes/caesar-cipher)

* For Vignere cipher:
    - [vigenere-solver](https://www.guballa.de/vigenere-solver)

* rot: [https://www.dcode.fr/rot-cipher](https://www.dcode.fr/rot-cipher)

* Substituion: [https://www.guballa.de/substitution-solver](https://www.guballa.de/substitution-solver)

* If you have no clue what the given cipher is then you can use the following:

    - [quipqiup](https://quipqiup.com/)
        + Don't use it if the given cipher contains lot of number.
        + It usually ignores number.

    - [I.C calculator](http://practicalcryptography.com/cryptanalysis/text-characterisation/index-coincidence/)
        + Differentiate between vignere, substitution.

For all the other type of cipher just look it on www.dcode.fr
It's got lot of decoders.

## XOR

Xor challenges are also very common in CTF. In some challenges might be directly about XOR like decode/brute-force the given xor cipher or in some challenges you might encounter XOR cipher as the final step or the starting step. In any case mostly you might have to bruteforce the cipher.


## AES

### ECB

So ECB is the mode which is generate a kind of pattern in it's encyrtion. Say we are using ECB for cookie purpose in a website now what we can do is register a user with name something like `aaaaa` and then take out the cookie. Then we can register a user with name like `aaaaaadmin`. Usually the auth cookie is specific to a user and envolves a user's name. Now say if it contains a pattern like `username <somerandom junk> passwords <maybe again some junk>`.

What we can do here is that we can find patterns by looking at the hex of the cookie. That would usually give away what kind of junk does the application uses. Once we have found the pattern or the number of bytes or padding we can make a cookie for the admin user and get the access.
 EX: https://pentesterlab.com/exercises/ecb/course
