I will try to make them in such a way that I can also share it with others as well. Hope this will be helpful for me as well as other people.

### General

These are my android notes that I am going to keep while I progress and see what all I can do.

- All the applications are stored on `/data/app` directory.
- All the system applications are stored on `/system/app/`
    - We don't have to touch this unless we are going behind the android OS
- Some application gets installed in `/data/app-private`
    - This is done my PM(package manager) using `FORWARD_LOCK` enabled
    - No external app or anyone else can access that.
    - Obviously if you have rooted device you can access those.

**zygotes**: This is the process that listen for new application requests in Android OS


* To get all the URLs from the apk
    -  `strings <apk> | grep -ProI "[\"'\`](https?://|/)[\w\.-/]+[\"'\`]"`

**Some general things**

- In *AndroidManifest.xml* we can see `<application>` tag they define layout and stuff but it have some spicy stuff as well
    - `<android:allowBackup>` : Define whether the backup of application data is allowed or not.
        - `run app.package.backup -f <package-name>`
        - So it's possible for the developer to define `Backupagent`  which can be used to do various task related to backup.
        - we can make the backup using `adb backup <package-name>` , an activity will be launched. Leave the Key field black and back it up
        - `dd if=backup.ab bs=24 skip=1 | openssl zlib -d > backup.tar`
            - here `backup.ab` is placed in the $(pwd)
        - extract the tar and see if the databases etc is also being shared.

    - Check if the app is debuggable:
        - `run app.pacage.debuggable`
        - If this is the case a shit load of information would be leaking.
        - Use `adb jdwp` to see what all application are running in debuggable mode.
        

## API keys

In 'strings.xml` you will find lot of APIs. It's possible to use some in wrong manners.

* Google Maps API key:
    - https://maps.googleapis.com/maps/api/staticmap?center=40.714728,-73.998672&zoom=12&size=2500x2000&maptype=roadmap&key=
    - Post the key and see it works.
    - Impact is not big but still an issue since an attacker can cause an increase in the cost.

## APK Signing

* **Generates X.509**

```jsx
keytool -genkey -v -keystore mykey.keystore -alias alias_name -keyalg RSA
-keysize 2048 -validity 10000
```

* **For Signing**

```jsx
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore
mykey.keystore application.apk alias_name
```

There are lot of bugs that have been discovered related to signing process. But those bugs are in the way android OS verifies the application and not in the application it self.%

