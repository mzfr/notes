# Misc

* If we want to add a in the sudoers file(/etc/sudoers):
    - `john ALL=(root) /command/that/is/allowed`
    - This would give user `john` the power to run the mentioned command as root
* If you need tor for python script:
    - https://www.sylvaindurand.org/use-tor-with-python/
* Remove a user from sudoer
    - `sudo deluser USERNAME sudo`
* Send message to another user
    - `mail -s "Your message" <username>`
    - EX: `mail -s "hey" www-data`
    - You might need to install mailutils to use `mail` command
* Restrict user to their own home directory
    - `sudo chown -R user:user userdir/`
    - `sudo chmod 0750 userdir/`
* If you want some kind of cronjob setup run
    - `crontab -e`
    - [crontab.guru](https://crontab.guru/)

* To make your own man page

```bash
$ cp nuseradd /usr/local/man/man8/nuseradd.8
$ gzip /usr/local/man/man8/nuseradd.8
$ man nuseradd
```

* Portknocking
    - https://blog.rapid7.com/2017/10/04/how-to-secure-ssh-server-using-port-knocking-on-ubuntu-linux/
    - http://technical-qa.blogspot.com/2014/10/solution-to-knockd-wont-work-open-port.html

## Python script to binary

* You can use `cython` or `nuitka` to compile python script to an elf.
    - nuitka does everything for you.
    - If using `cython` then do the following:
        * `cython file.py --embed`
            - use `-3` or `-2` to use python versions
        * `gcc -Os -I /usr/include/python3.5m -o file file.c -lpython3.5m -lpthread -lm -lutil -ldl`

## Fixing interface name

* When we need to fix the damn interface name so dynamic dhcp is working
    - https://mzfr.github.io/interface-names

## Add a new user:

```bash
sudo adduser <username>
```

## Setting up FTP server

* Install vsftpd
    - `sudo apt install vsftpd`
* make a backup copy of the config file.
    - `cp /etc/vsftpd.conf /etc/vsftpd.conf.orig`
* Edit the options accordingly

* https://www.tecmint.com/install-ftp-server-in-ubuntu/
* https://www.digitalocean.com/community/tutorials/how-to-set-up-vsftpd-for-anonymous-downloads-on-ubuntu-16-04

## Edit /etc/issue

To be able to display the IP of the machine right when it starts you can edit /etc/issue

```
IP: \4{eth0}
```


This only display the IP and if you want something else you can add that too like the name of the machine or something else.


## Setup Wordpress

The best thing is to follow this article

https://www.tecmint.com/install-wordpress-on-ubuntu-16-04-with-lamp/

Make sure to verify which is the latest version for PHP and wordpress.

## Setting up virtual hosts on apache2

* Install apache2 and then in `var/www/html` will be the default.
* Now in `/etc/apache2/sites-available` do the following:
    - `cp 000-default.conf <name-of-virtual-host>.conf`
* Open that newly creadted `.conf` file and make changes to `DocumentRoot` and `ServerName` values.
    - `DocumentRoot` -  this will be the directory which will have the files for the virtual host
    - `ServerName` - URL/IP/Domain on which this has to be accessed.

```
ServerAdmin webmaster@localhost
ServerName mehtab.zafar.tech
DocumentRoot /var/www/sites     
```

here when someone try to visit `mehtab.zafar.tech` then the apache will use files from `/var/www/sites` else for other domain/IP it will use the default configuration.

* Run the following command:

```
a2ensite <name-of-the-conf-without-extension>
```
Ex: `a2ensite mehtab` - where configuration file name was `mehtab.conf`

* Now just restart apache

## Setting up Postgres

To install postgres on ubuntu you can run:
```
sudo apt install postgresql
```

After that you can login as `postgres` user and create DB or add users.

- To login as postgres run: `sudo -u postgres psql`
- Then you can run following commands to create a new DB and add a new USER which have GRANT on that DB.

```
create database <DB_NAME>;
create user <USERNAME> with password encrypted password '<your-password>';
grant all privileges on database <DB_NAME> to <USERNAME>;
```
 ### Extra commands in psql

 * `\l` - list all DB
 * `\du` - list all users
 * `\c <DBNAME>` - Use the specified DB
