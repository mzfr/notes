So these are just collections of command that might be helpful.

### adb

- To find the package
    - `adb shell pm list packages | grep <package-name>`
    - If you have frida server running you can run `frida-ps -U | grep <name>`

### drozer

These commands are to be run on drozer console which open by running: `drozer console connect`

- Package info: `run [app.package.info](http://app.package.info) -a <package-name>`
- To open **AndroidManifest.xml:** `run app.package.manifest <package-name>`
    - It's better to open this file in your editor to be able to read through it properly 😃
- To see how many activity, broadcast, service or content provider are exported run:
    - `run app.package.attacksurface <package-name>`
- See clipboard content
    - `module install clipboard`
    - `run post.capture.clipboard`
