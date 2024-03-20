# esp-open-sdk
forked from 
<a href="https://github.com/pfalcon/esp-open-sdk">pfalcon/esp-open-sdk</a>
<br>
## Tested on Ubuntu22.04

```
 su -c " \
 apt update ; \
 apt-get install -y make unrar-free autoconf automake libtool gcc g++ gperf \
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

```
FROM ubuntu:22.04 as builder

RUN groupadd -g 1000 docker && useradd docker -u 1000 -g 1000 -s /bin/bash -d /build
RUN mkdir /build && chown docker:docker /build

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt-get install -y \
      make unrar-free autoconf automake libtool gcc g++ gperf \
      flex bison texinfo gawk ncurses-dev libexpat-dev \
      python3-dev python3 python3-serial python-is-python3 \
      sed git unzip bash help2man wget bzip2 libtool-bin 


# Checkout main source code
RUN su docker -c " \
    git clone --recursive https://github.com/LouisLee985/esp-open-sdk.git /build/esp-open-sdk ; \
"

# Patch source code to make it work on newer Linux version
RUN su docker -c " \
    cd /build/esp-open-sdk ; \
    cd esptool ; \
    git checkout v1.3 ; \
"

# Build code
RUN su docker -c "cd /build/esp-open-sdk && make STANDALONE=n"

FROM ubuntu:22.04

RUN DEBIAN_FRONTEND=noninteractive apt update && \
    DEBIAN_FRONTEND=noninteractive apt install -y make python3 python3-serial

COPY --from=builder /build/esp-open-sdk/xtensa-lx106-elf /opt/xtensa-lx106-elf
ENV PATH /opt/xtensa-lx106-elf/bin:$PATH
```
## Thanks
<br>1.　https://github.com/maximkulkin/esp-homekit-demo/wiki/Build-instructions-ESP8266-(Docker)
<br>2.　https://github.com/pfalcon/esp-open-sdk/pull/391
