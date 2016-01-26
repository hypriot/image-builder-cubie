# image-builder-cubie
[![Join the chat at https://gitter.im/hypriot/talk](https://badges.gitter.im/hypriot/talk.svg)](https://gitter.im/hypriot/talk?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


This is work in progress and not yet finished.

This is to evaluate if the cubieboard and cubietruck can use the same image.
As first approach this repo is a copy of out odroid-xu4 repo (both use uboot ...).


# Setting up build environment
Make sure you have [vagrant](https://docs.vagrantup.com/v2/installation/) and [docker-machine](https://docs.docker.com/machine/install-machine/) installed.

A `vagrant up` in the root folder of this repository sets up a Ubuntu Trusty VM with the latest Docker installed.

To use this Docker instance from your host one can use `docker-machine`.  
To set it up with your Vagrant VM execute the following command:

```bash
docker-machine create -d generic \
  --generic-ssh-user $(vagrant ssh-config | grep ' User ' | awk '{print $2}') \
  --generic-ssh-key $(vagrant ssh-config | grep IdentityFile | awk '{gsub(/"/, "", $2); print $2}') \
  --generic-ip-address $(vagrant ssh-config | grep HostName | awk '{print $2}') \
  --generic-ssh-port $(vagrant ssh-config | grep Port | awk '{print $2}') \
  image-builder-odroid-xu4
```

Now set the Docker environments to this new docker machine:

```bash
eval $(docker-machine env image-builder-odroid-xu4)
```

From here just use `make` to make a new SD-Card image:

```bash
make sd-image
```
