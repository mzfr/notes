They are responsible for providing you all the notifications that you get. Also sometimes they pass around bits and pieces of information to other/multiple applications.

- `run [app.broadcast.info](http://app.broadcast.info) -a <package-name>`
- Broadcasts are sent via `sendBroadcast()` and what will be done on that broadcast will be determined by `onReceive()` method.
- There are broadcasts receivers that gets registered at runtime so drozer will not report them and you'll have to find them manually.
    - `registerReceiver()` - This is the method name.
- It's possible that a activity have a intent filter. Now if we pass the intent via a broadcast it's possible that activity might get provoked.
    - Only happens when it's set to `exported=True` or you have root permission(N/A)
- We can also try to sniff the broadcasts.
    - `run app.broadcast.sniff -a <action/intent>`
