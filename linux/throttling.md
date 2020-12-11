---
description: Thermal daemon caused my Ubuntu 16.04 to throttle
---

# Throttling

I fixed it by 

* Removing the Ubuntu default thermal daemon
* cloning [https://github.com/intel/thermal\_daemon](https://github.com/intel/thermal_daemon)
* Building and installing the updated daemon

Unfortunately I don't have the links saved, but there were some bug reports available on thermal daemon causing problems.

