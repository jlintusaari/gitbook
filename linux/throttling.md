---
description: Links and resources fixing various issues with Ubuntu 16.04
---

# Various issues

### Mouse sensitivity

{% embed url="https://askubuntu.com/questions/8506/decrease-mouse-sensitivity-below-the-standard-limit" %}

```text
# .bashrc

# Find the external mouse id
# Lines not containing DELL but containing Mouse or M325 and just print the \2 group containing the numeric id
XID=$(xinput | sed -n '/DELL/! s/.*\(Mouse\|M325\).*id=\([0-9]*\).*/\2/p')
if [ ! -z "$XID" ]; then
    echo "Modifying xinput for Mouse $XID"
    xinput set-prop $XID "Device Accel Profile" -1
    xinput set-prop $XID "Device Accel Constant Deceleration" 1.8
fi

```

### System shortcut issues with JetBrains IDE:s

[https://stackoverflow.com/questions/44871910/how-to-disable-alt-f-e-v-menu-shortcuts-in-intellij](https://stackoverflow.com/questions/44871910/how-to-disable-alt-f-e-v-menu-shortcuts-in-intellij)

### Thermal daemon caused Ubuntu 16.04 to throttle

I fixed it by 

* Checking cpu utilization levels under CPU intensive task: `lscpu | grep MHz` \(if they are not 100 % then throttling is occurring\)
* Removing the Ubuntu default thermal daemon  `sudo systemctl disable thermald && sudo reboot`
* cloning [https://github.com/intel/thermal\_daemon](https://github.com/intel/thermal_daemon)
* Building and installing the updated daemon

Unfortunately I don't have the links saved, but there were some bug reports available on thermal daemon causing problems.

