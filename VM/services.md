# Runing Services on startup

__In my experience it's better to use systemd rather then putting your head under this supervisor setup__

## Supervisor

* For supervisor when you want to autostart some service on boot

https://gist.github.com/mozillazg/6cbdcccbf46fe96a4edd

```
[program:name]
directory=/opt/1337
command=flask run --port 1337
autostart=true
autorestart=true
stopsignal=INT
stopasgroup=true
killasgroup=true
```

Then restart the `supervisor` service
```bash
sudo systemctl restart supervisor.service
```

And then you can check if the service is running by executing
```
supervisorctl status
```

You should see the new app.

Sometime we end up getting error like
```
unix:\\\var\run\supervisor.sock no such file
```

or

```
error: <class socket.sock>..........
```

So the fix that seemed to work for me was to run `echo_supervisord_conf > /etc/supervisor/supervisord.conf `

and then reread the config with

```
supervisorctl -c /etc/supervisord/supervisord.conf reread
```

and then we should see all the services running.

## Systemd service file

In my experience it's better to just make a `<name>.service` file in `/etc/systemd/system` to setup a service rather than trying to mess with supervisor.

### Xinetd

If you want something to do with shells or a service accesible via `nc`/`telnet` then it's better to setup a `xinetd` service.

- https://www.cyberciti.biz/faq/linux-how-do-i-configure-xinetd-service/

- Sometimes when you start the xinetd service you might get an error about `no service game/tcp` etc if this is the case just open `/etc/services` and add your service name with the port you are running it on.

```
game        1337/tcp        #this is a game
```

Here `game` is the name of the service and `1337` is the port on which it is running. Text after `#` is just a comment.


### Other application with Systemd

This is just an example of `flask` application but in the similar manner you can run any other service as well. Ex: `apache2`

- https://blog.miguelgrinberg.com/post/running-a-flask-application-as-a-service-with-systemd

Basically make a file named `whatevernameyouwant.service` in `/etc/systemd/system` and write this:

```
[Unit]
Description=web application
After=network.target

[Service]
User=www-data
WorkingDirectory=/opt/webapp
ExecStart=/bin/bash -c "/usr/local/bin/flask run --host 0.0.0.0 --port 80 "
Restart=always

[Install]
WantedBy=multi-user.target
```

