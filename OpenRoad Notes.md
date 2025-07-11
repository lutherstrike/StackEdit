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
           --security-opt seccomp=unconfined 
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
`export JAVA_OPTS="-Djavax.net.ssl.trustStore=/usr/lib/jvm/java-21-openjdk-amd64/lib/security/cacerts"`
(its stupid, why!!!!!)

Downloading of `firtool` is timed out some unknown reason. 
Installing `firtool` binary manually. Different Chisel versions have different minimum version of Firtool requirement. Latest Firtool should be enough. Firtool is FIRRTL (Flexible Intermediate Representation for RTL) compiler of CIRCT,  so it depends on LLVM/MLIR

Z3, sbt and Verilator are installed to `/usr/local/bin` or `/usr/local/lib`

Related setting:

```sh
export Z3_LIBRARIES=/usr/lib/x86_64-linux-gnu/libz3.so
export PATH=$PATH:/home/xingyu/tools/circt/build/bin
export CHISEL_FIRTOOL_PATH=/home/xingyu/tools/circt/build/bin
```

## Flow notes
OpenRoad test with customized Verilog code


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MzIzMTY0MzYsMTIwOTM3MDM0OCwxNz
UzNzcyMDQ4LDEzMTc1MTU5NzMsMTA2NjM2OTA1NSwxMjY1OTAz
NDYyLDE3MzMzMzMzNTAsMTI2NTkwMzQ2MiwxNDU3MjI5NjIyLD
IxMDUwNjY2ODUsLTc3Mjg1MzQ0NSw2NjQyNjkxMjgsMjAyODcz
Nzc2OSwtMjAxNTc2NzM4OCwxNTI4NDQzODQwLDEyMjE5NDE5Mj
IsMjQ5OTgyODAwLDM2ODA3NDUwMSw1NjA4NTY4ODIsMTg3NTEz
NjYyNF19
-->