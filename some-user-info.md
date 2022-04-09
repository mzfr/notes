If you remove a user, but leave their sudo privileges in place, can a user be created with that same name and exploit the sudo privileges?

The answer is yes.

Created test1 user

Gave test1 sudo access to apt-get

User freddy had access to be able to use adduser and deluser.

Freddy deleted test1 user - deluser --home-remove test1 - and then added a new test1 user and gave it a password.

Freddy then did a su to test1, and ran the following:

sudo apt-get changelog apt
!/bin/sh

---

#includedir /etc/sudoers.d
test1 ALL=(ALL) NOPASSWD: /usr/bin/apt-get
freddy ALL=(ALL) NOPASSWD: /usr/sbin/adduser,/usr/sbin/deluser

---

#includedir /etc/sudoers.d
%helpdesk ALL=(ALL) NOPASSWD: /usr/bin/apt-get
freddy ALL=(ALL) NOPASSWD: /usr/sbin/adduser,/usr/sbin/deluser

---

Add group helpdesk
groupadd helpdesk

Create user and add to helpdesk group
sudo adduser test2
sudo adduser test2 helpdesk

#includedir /etc/sudoers.d
%helpdesk ALL=(ALL) NOPASSWD: /usr/bin/apt-get
freddy ALL=(ALL) NOPASSWD: /usr/sbin/adduser,/usr/sbin/deluser

---

Problem with last version, is that user can add themselves to the helpdesk group and then log off and back on with sudo privs of helpdesk.

---

sudo adduser test2
sudo adduser test2 helpdes
