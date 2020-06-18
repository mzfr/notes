# Intents

Basically a data object that tells what task is to be performed.

```jsx
<activity android:name="ActivityName">
    <intent-filter>
	<action android:name="android.intent.action.View">
	<android:scheme="http">
    </intent-filter>
</activity>
```

This is a simple activity telling about the `action` and the type of URL it accepts. The scheme of that URL can be `http`.

*There are Explicit intent as well - They are sort of one that opens the URL in the android browser. Think of like when you click on some article link in twitter app and it opens, In-app Browser.*

```jsx
**run app.activity.start —action <activity-name> —data-uri <URL> —component <component> <package-name>**
```

This is the command that can be used to interact with acitivites using drozer.

**NOTE**: Always make sure to check out the code of that Activity to see what it is doing with the URL and see if it can be exploited.

- Review the source code that handles the exported intents