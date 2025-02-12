## Installation
**OpenRoad**
Final solution: use `latest` image from the official publisher with `root`privilege.

+ Mobaxterm [notes](https://blog.mobatek.net/post/how-to-keep-X11-display-after-su-or-sudo/) for open gui with `sudo`.
+ Open GUI without `root` inside the docker will cause crash/segmentation fault.

Setup for network:
+ `/etc/cntlm.conf` for the proxy servive setup
+ Copy Huawei certificate, then update the docker file with proxy.
All files backup are in `~/setup`.

Command to start the container from the official image (different from the doc):
```bash
docker run --rm -it \
           -e DISPLAY=${DISPLAY} \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -v ${HOME}/.Xauthority:/root/.Xauthority \
           --network host \
           --security-opt seccomp=unconfined \u
           openroad/flow-ubuntu22.04-builder bash
# No need to mount the examples since the offical image already has all sources

#defualt comand
docker run --rm -it \
		   -v $(pwd)/flow:/OpenROAD-flow-scripts/flow \
           -e DISPLAY=${DISPLAY} \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -v ${HOME}/.Xauthority:/root/.Xauthority \
           --network host \
           --security-opt seccomp=unconfined \
           openroad/flow-ubuntu22.04-builder bash
```
**Chisel**


## Flow notes 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzY4MDc0NTAxLDU2MDg1Njg4MiwxODc1MT
M2NjI0LC0xNDMxMjUxOTUyLC0xMDYwMTE5NjUsLTczNjQyNjAw
MCwtMTc2NTc4OTE4MiwtMTI1NDA3MjM2NCwtMTEzODYwODMwMi
wxNDc0NDk2NDU4LDkzODE5ODY2OCwtMTM0NzQ2NTk1NSwxNjky
OTE5Njk2XX0=
-->