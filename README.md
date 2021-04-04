# Scripts supporting Docker Secrets

Included are two scripts:
1. `01_secret-init.sh`, a Bourne shell (`sh`) script 
2. `01_s6-secret-init.sh`, a Bourne shell script to run in S6 container environments

Credit to (linuxserver.io)[https://github.com/linuxserver/docker-baseimage-ubuntu/blob/bionic/root/etc/cont-init.d/01-envfile], the source of the logic for these scripts


## Integrating into containers
Scripts must be added to Docker image and called at container launch.

If using `secret-init.sh`, you can either:
* Run script as `CMD` or `ENTRYPOINT` from the Dockerfile
* Run script from an init script, where the init script is run via `CMD` or `ENTRYPOINT`
```
# dockerfile excerpt
COPY secret-init.sh /usr/local/bin/
ENTRYPOINT [ "docker-entrypoint.sh" ]
```


If using `s6-secret-init.sh, simply copy the script to `/etc/cont-init.d/` when building the Docker image, and S6 will automatically run the script as part of container init.
```
# dockerfile excerpt
COPY 01_envfile.sh /etc/cont-init.d/
```
