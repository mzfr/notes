These are the third party application which can access the data from the application or provide it with some sensitive data. Ex: Like an app providing login via Facebook would have an activity that provokes the facebook login and stuff. After that facebook SDK would handle everything and once validated it will give the main application all the data required.

The main issue with content provider activity is that they do not mention `android:exported=false` explicitly. If on any Content providers exported is set to true or is not mentioned at all then it could be vulnerable. It's sometime possible that they are exported but if that is the case then check that they are given certain permission. If they are exported and have `null` permission then that could be a big issue.

- `run app.provider.finduri <paackage-name>`
    - This will give you all the URLs that are accessible.
    - Then you can run: `run app.provider.query <URL>` to see what data it returns.
    - If this could be done then using `app.provider.insert` we can insert new data information.
- With drozer you can also try to detect for SQL injection
    - `run scanner.provider.injection -a <URI>/<pacckage-name>`
- Also you can test whether the content provider allows the retrieval of files.
    - `run [app.provider.read](http://app.provider.read) <content-provider-URL> /system/etc/hosts`
    - file `/system/etc/hosts` is always present and word readable.
        - It's like checking LFI by including `/etc/passwd`
            - The vulnerability here is that if you can include a system file then you can read file from databases etc.
- It's possible that pattern problems exists. If a content provider uses `path` in `path-permission` that means only that path is protected. So say `path=/Keys` was used that mean only that path is protected and it's possible that we can access the `/Keys/` path.
    - Try to see whether the developer have used full path or not.
    - Think like in linux systems when people use just the binary name and doesn't give full path we exploit that by making binary of that name and adding in `/tmp/` and then adding that path to the $PATH
