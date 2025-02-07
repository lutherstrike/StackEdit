## Installation
Final solution: use `latest` image from the official publisher with `root`privilege.

+ Mobaxterm [notes](https://blog.mobatek.net/post/how-to-keep-X11-display-after-su-or-sudo/) for open gui with `sudo`.

Setup for network:
+ `/etc/cntlm.conf` for the proxy servive setup
+ Update the docker file with proxy and huawei certificate

Command to start the container from the official image (different from the doc):
```bash
docker run -it \
           
           -e DISPLAY=${DISPLAY} \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -v ${HOME}/.Xauthority:/root/.Xauthority \
           --network host \
           --security-opt seccomp=unconfined \
           openroad/flow-ubuntu22.04-builder bash
# No need to mount the examples since the offical image already has all sources
# -v $(pwd)/flow:/OpenROAD-flow-scripts/flow \

```

## Flow notes 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMzg2MDgzMDIsMTQ3NDQ5NjQ1OCw5Mz
gxOTg2NjgsLTEzNDc0NjU5NTUsMTY5MjkxOTY5Nl19
-->