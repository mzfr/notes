To setup fail2ban on ubuntu for the SSH port we do the following:

### Installation

* `apt install fail2ban`
* Allow SSH through ufw
    - `ufw allow ssh`
    - `ufw enable`

### Configuration

* Move the default config file:
    - `cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local`

* Now we can start editing the local copy we made. You can choose not to edit it since the default config is also pretty solid.

* Now we can configure the `jail` setting.
    - `cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`
    - now make changes to the local jail file as desired.
