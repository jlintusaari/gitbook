---
description: How to run GUI programs from a Docker container.
---

# X11 sharing

### How to run desktop apps within docker

This content is adapted from the following link:

{% embed url="http://fabiorehm.com/blog/2014/09/11/running-gui-apps-with-docker/" %}

Dockerfile:

```text
FROM ubuntu:18.04

# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /etc/sudoers.d && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer
CMD /bin/bash

```

After this you need to start the container with:

```text
docker build -t x11 .

docker run -ti --rm \
       -e DISPLAY=$DISPLAY \
       -v /tmp/.X11-unix:/tmp/.X11-unix \
       x11
       
```

Within the container you can install and launch GUI programs, such as firefox.

