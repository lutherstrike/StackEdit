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
Chisel is a Scala lib and Scala-cli is using JVM. 
However, after adding huawei certificates to its default truststore, it's not using it correctly. You have to add env variable like this (or java parameter):
`export JAVA_OPTS="-Djavax.net.ssl.trustStore=/usr/lib/jvm/java-21-openjdk-amd64/lib/securi
ty/cacerts"`
(its stupid, why!!!!!)

Downloading of `firtool` is timed out some unknown reason. 
Installing `firtool` manually.
## Flow notes 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUyODQ0Mzg0MCwxMjIxOTQxOTIyLDI0OT
k4MjgwMCwzNjgwNzQ1MDEsNTYwODU2ODgyLDE4NzUxMzY2MjQs
LTE0MzEyNTE5NTIsLTEwNjAxMTk2NSwtNzM2NDI2MDAwLC0xNz
Y1Nzg5MTgyLC0xMjU0MDcyMzY0LC0xMTM4NjA4MzAyLDE0NzQ0
OTY0NTgsOTM4MTk4NjY4LC0xMzQ3NDY1OTU1LDE2OTI5MTk2OT
ZdfQ==
-->