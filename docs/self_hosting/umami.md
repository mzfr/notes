Initially I was hosting [umami](https://github.com/umami-software/umami) on a digitalocean server but then I realized I can host it on fly.io without any cost at all. So I moved my umami instance from a digitalocean droplet to fly.io

# How to

* Get an account on fly.io
* Install flyctl - https://fly.io/docs/hands-on/install-flyctl/
* Once it's installed run fly launch, go through the options and in the end it will generate a fly.toml file.
* Replace the content of the toml file with the following:

```toml
app = "falconfeast-umami"
kill_signal = "SIGINT"
kill_timeout = 5
processes = []

[build]
  image = "ghcr.io/umami-software/umami:postgresql-latest"

[env]
  DATABASE_TYPE = "postgresql"
  DATABASE_URL = "$DATABASE_URL"
  DISABLE_UPDATES = 0

[experimental]
  allowed_public_ports = []
  auto_rollback = true

[[services]]
  http_checks = []
  internal_port = 3000
  processes = ["app"]
  protocol = "tcp"
  script_checks = []
  [services.concurrency]
    hard_limit = 25
    soft_limit = 20
    type = "connections"

  [[services.ports]]
    force_https = true
    handlers = ["http"]
    port = 80

  [[services.ports]]
    handlers = ["tls", "http"]
    port = 443

  [[services.tcp_checks]]
    grace_period = "1s"
    interval = "15s"
    restart_limit = 0
    timeout = "2s"
```

* Deploy a postgres instance

```bash
fly postgres create
```

* Once the postgres instance is deployed and you have a the URL to connect to it.
* Connect to the pg instance and create a new user along with a DB
  - I had issues directly connecting to the pg instance, so I connect to the fly's proxy and then connected to the postgres instance.

```
# Connect to the proxy
fly proxy 5432 -a <YOUR_DB_NAME>

# Connect to the PG instance 
fly pg connect -p <DB_PASSWORD> -u <DB_USER> -a <DB_NAME>
```

* Once connected create a new user and a DB for umami to store data
* After that you can create a fly's secret, the one we have in our fly.toml file i.e DATABASE_URL

```bash
fly secret set DATABASE_URL=<YOUR_DB_URL>
```

* In the end you can deploy the application by running: `fly deploy`

***

Once that is done you can create a custom domain from fly's dashboard.
