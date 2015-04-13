# Boot2Docker

I forked the original repository and followed the following guide to rebuild Boot2Docker and make it able to write to OSX folders:
## ~~~~~~~~~~~~~~~~~~~~~~~~~~~
I built my own Boot2Docker iso that mounts filesystems with more liberal permissions, it was very easy:

Clone https://github.com/boot2docker/boot2docker

Edit `rootfs/rootfs/etc/rc.d/automount-shares` and change the line that says:

```console
mountOptions='defaults'
```
to

```console
mountOptions='defaults,dmode=777,fmode=666'
```
Then build the image with your existing boot2docker installation and write the iso to the current directory:

```console
docker build -t boot2docker . && docker run --rm boot2docker > boot2docker.iso
```
Then you can destroy your current boot2docker vm: `boot2docker stop && boot2docker delete`

Then copy the new iso to your ~/.boot2docker directory: `cp boot2docker.iso ~/.boot2docker`

Then re-init your boot2docker VM: `boot2docker init && boot2docker up`

There you go, when you ssh into your boot2docker vm now, all the directories will be 777 and files will be 666.
## ~~~~~~~~~~~~~~~~~~~~~~~~~~~

Source: https://github.com/docker-library/mysql/issues/44#issuecomment-73331030
