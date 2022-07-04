* We can enable Bluetooth HCI logging from developers options and then do some BLE stuff and there will be a file called `btsnoop_hci.log`.

* `/etc/bluetooth/bt_stack.conf` is the file that hold all the information about the bluetooth configuration.
    - If rooted phone: `adb shell su` gives you the root access
        + But even then we cannot edit that file manually.

* Chances are that we might not be able to directly pull the `btsnoop_hci.log` via `adb pull <path to the file>`.
    - Best solution is to get sudo shell and copy that file to `/sdcard`
    - Then run `abd pull /sdcard/btsnoop_hci.log`
