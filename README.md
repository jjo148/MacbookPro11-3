# MacbookPro11-3
Misc configs for setting up Linux on Apple Macbook Pro 11,3

## Power / Suspend
#
**Fix CPU refusing to suspend, aka "cache: CPU # should not be sleeping"-warning.**

src: https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1574125/comments/71

Create file:

$ *sudo nano /lib/systemd/system-sleep/sleepcpu*

```
#!/bin/bash
# File: /lib/systemd/system-sleep/sleepcpu

case "$1" in
    pre)
 for c in /sys/devices/system/cpu/cpu*/online; do echo 0 >$c; done
        ;;
    post)
 for c in /sys/devices/system/cpu/cpu*/online; do echo 1 >$c; done
        ;;
esac

Save it, and:

$ sudo chmod +x /lib/systemd/system-sleep/sleepcpu
```

#

**Fix spurious wakeup from sleep/suspend**

Disable ACPI *wakeup* event from *USB 3.0 Hi-Speed/SuperSpeed Bus*:
```
$ echo XHC1 > /proc/acpi/wakeup
```

#
## Display backlight

Install package **acpilight-git** from AUR
