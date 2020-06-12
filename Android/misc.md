* To get all the URLs from the apk
    -  `strings <apk> | grep -ProI "[\"'\`](https?://|/)[\w\.-/]+[\"'\`]"`

## API keys

In 'strings.xml` you will find lot of APIs. It's possible to use some in wrong manners.

* Google Maps API key:
    - https://maps.googleapis.com/maps/api/staticmap?center=40.714728,-73.998672&zoom=12&size=2500x2000&maptype=roadmap&key=
    - Post the key and see it works.
    - Impact is not big but still an issue since an attacker can cause an increase in the cost.

## URLS

If any Firebase URL is found, try to add `.json` and see if it returns anything. If it gives `permission denied` then nothing to do. But if you get some data there meaning $$$$$


* In adb we can access the exported activities separately. So in the androidmanifest.xml if there is any activity that is being exported i.e `android:exported="true"` then we can do the following:

    - `adb shell am start -n <package-naem>/.<activity_name>`

* Check strings.xml

