## Rules

These are the must do's and don'ts of making the boot2root machine.

* Always link `.bash_history` file to `/dev/null`
    - `ln -sf /dev/null .bash_history`

* If you for some reason used your SSH key to easily access the VM for testing or any other purpose make sure to remove it.

* Test your VM with lowest possible hardware configuration so you know when your thing will crash.

* Make sure to thoroughly test all the things so that you don't mess up.
    - If you want other people to test your VM then contact [m0tleycr3w](https://m0tleycr3w.github.io/)
        + I get all my VMs test by them :-)
