# Intercept

One of the important thing is that a person should be able to intercept data from a network and see if there is something interesting.

* `sudo tcpdump -i `INT` udp port 53`
    - `INT` is the interface you want to listen on. For example, eth0.
    - udp port 53 is used to only sniff UDP packets on port 53 (to keep DNS queries).
        -  we can make it for anything.
    - This command would tell you what kind of DNS is victim trying to access, if we can get that then we can spoof the DNS and get the information, basically a MiTM attack.

* You can also setup a server with fake TLS cert and just get control of DNS resolution to read HTTPS content.
    - Obviously this only works when client isn't checking the validity of the TLS cert.
    
