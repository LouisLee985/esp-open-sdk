# esp-open-sdk
forked from 
<a href="https://github.com/pfalcon/esp-open-sdk">pfalcon/esp-open-sdk</a>
<br>
## Tested on Ubuntu22.04

```
 su -c " \
 apt update ; \
 apt install -y make unrar-free autoconf automake libtool gcc g++ gperf \
      flex bison texinfo gawk ncurses-dev libexpat-dev \
      python3-dev python3 python3-serial python-is-python3 \
      sed git unzip bash help2man wget bzip2 libtool-bin "
```

```	
 git clone --recursive https://github.com/LouisLee985/esp-open-sdk.git ; \
 cd esp-open-sdk/esptool ; \
 git checkout v1.3 ; \
 cd .. ; \
 make toolchain esptool libhal STANDALONE=n
```

## Tested on Docker
```shell
docker run -it --name esp-open-sdk jslzlai/esp-sdk:0.1 /bin/bash
```
---
<br>1.  https://github.com/LouisLee985/esp-open-sdk/wiki
<br>2.　https://github.com/maximkulkin/esp-homekit-demo/wiki/Build-instructions-ESP8266-(Docker)
<br>3.　https://github.com/pfalcon/esp-open-sdk/pull/391
