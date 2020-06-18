# Permissions

So every app asks for permission and each permission is defined in the *AndroidManifest.xml*

Ex: If an app is asking for `Read SMS` then it would be defined something like: `android.permission.READ_SMS`

We can use **drozer** command to see such kind of permissions:

```jsx
run app.package.info -a <package-name>
```

Also we can search application which is requesting particular permission:

```jsx
run app.package.list -p android.permission.READ_SMS
```

Example:

```jsx
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" android:maxSdkVersion="18"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" android:maxSdkVersion="18"/>
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE"/>
    <uses-permission android:name="android.permission.WAKE_LOCK"/>
```

This is from on android application.

- If `android:exported` is not defined then the version of SDK or the version of Android will determine whether it's `true` or `false`
- Any component using `intent-filter` is exported by default.