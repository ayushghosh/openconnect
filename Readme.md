
[![Build Status](https://travis-ci.org/robertbeal/openconnect.svg?branch=master)](https://travis-ci.org/robertbeal/openconnect)
[![](https://images.microbadger.com/badges/image/robertbeal/openconnect.svg)](https://microbadger.com/images/robertbeal/openconnect "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/robertbeal/openconnect.svg)](https://microbadger.com/images/robertbeal/openconnect "Get your own version badge on microbadger.com")
[![](https://img.shields.io/docker/pulls/robertbeal/openconnect.svg)](https://hub.docker.com/r/robertbeal/openconnect/)
[![](https://img.shields.io/docker/stars/robertbeal/openconnect.svg)](https://hub.docker.com/r/robertbeal/openconnect/)
[![](https://img.shields.io/docker/automated/robertbeal/openconnect.svg)](https://hub.docker.com/r/robertbeal/openconnect/)

Built from https://github.com/dlenski/openconnect to get the additional Palo Alto Networks (PAN) authentication mode.

The below example uses `--read-only` mode (for a tiny bit of additional security). You will get errors that it can't flush or backup resolv.conf (both part of the vpnc script) but it all still works just fine. 

Use `-e ARGS=` for passing in command line parameters. 

```
docker run \
	--name openconnect \
	--net host \
	--read-only \
        --tmpfs /var/run/vpnc \
	--cap-add=NET_ADMIN \
	--device /dev/net/tun \
        -v /etc/resolv.conf:/etc/resolv.conf \
        -e ARGS="--protocol=gp <ip> --servercert sha256:<sha>" \
	-it robertbeal/openconnect:latest
```
