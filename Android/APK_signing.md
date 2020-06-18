# APK signing

**Generates X.509**

```jsx
keytool -genkey -v -keystore mykey.keystore -alias alias_name -keyalg RSA
-keysize 2048 -validity 10000
```

**For Signing**

```jsx
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore
mykey.keystore application.apk alias_name
```

There are lot of bugs that have been discovered related to signing process. But those bugs are in the way android OS verifies the application and not in the application it self.