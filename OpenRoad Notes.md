## Installation
Final solution: use `latest` image from the official publisher with `root`privilege.

+ Mobaxterm [notes](https://blog.mobatek.net/post/how-to-keep-X11-display-after-su-or-sudo/) for open gui with `sudo`.

Setup for network:
+ `/etc/cntlm.conf` for the proxy servive setup
+ Update the docker file with proxy and huawei certificate

Co
```bash
docker run -it \
	     -u $(id -u ${USER}):$(id -g ${USER}) \
           -v $(pwd)/flow:/OpenROAD-flow-scripts/flow \
           -e DISPLAY=${DISPLAY} \
           -v /tmp/.X11-unix:/tmp/.X11-unix \
           -v ${HOME}/.Xauthority:/root/.Xauthority \
           --network host \
           --security-opt seccomp=unconfined \
           openroad/flow-ubuntu22.04-builder bash

```

## Flow notes 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyODM2NTcyMiw5MzgxOTg2NjgsLTEzND
c0NjU5NTUsMTY5MjkxOTY5Nl19
-->