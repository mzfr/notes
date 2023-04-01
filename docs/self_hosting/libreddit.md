[libreddit](https://github.com/libreddit/libreddit) is a self hostable frontend for reddit. And to be honest ever since I have came across it I've have not used the reddit's main or old website at all.

So I basically hosted an instance for myself via [fly.io](https://fly.io/). The reason for hosting on fly.io is that they allow upto 3 CPU applications be hosted for free and also running libreddit on it was really easy.

# How to

* Get an account on fly.io
* Install flyctl - https://fly.io/docs/hands-on/install-flyctl/
* Once it's installed run `fly launch`, go through the options and in the end it will generate a `fly.toml` file.
* Replace the content of the toml file with the following:

```toml
app = "<YOUR_APP_NAME>"
kill_signal = "SIGINT"
kill_timeout = 5
processes = []

[build]
  image = "libreddit/libreddit"

[env]

[experimental]
  auto_rollback = true

[[services]]
  http_checks = []
  internal_port = 8080
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

* Run `fly deploy`.

***

I use [libredirect](https://github.com/libredirect/libredirect) to automatically redirect every www.reddit.com or old.reddit.com URL to my own instance of libreddit.

**My Instance** - https://reddit.zfr.sh
