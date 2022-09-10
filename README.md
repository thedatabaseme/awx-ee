# thedatabaseme AWX EE

This repository contains building instructions for a self-build AWX execution environment.
To find detailed instructions and information about why to use your own build EE might
be a good idea, you can find a blog article of me [here](https://thedatabaseme.de/2022/09/09/self-build-awx-execution-environment/).

[![Build nightly AWX EE image](https://github.com/thedatabaseme/awx-ee/actions/workflows/nightly-build.yml/badge.svg?branch=develop)](https://github.com/thedatabaseme/awx-ee/actions/workflows/nightly-build.yml)

# Build instructions

To build this execution environment image by yourself (you can also use the image that is
linked to this repository), follow the steps below.

You need to have ansible-builder installed on your building machine. You can do so by the
following command:

```
pip install ansible-builder
```

Clone this repository to a location of your choice and trigger the `ansible-builder` 
command to build yourself a container image.

```
ansible-builder build --tag thedatabaseme/awx-ee:0.0.1 --container-runtime docker -f execution-environment.yml
```

If you run podman as your container runtime on your system, you can leave out the
`--container-runtime` option cause podman is the default CR.

## Local testing

After building, you may want to test your locally build image. You can do so by creating
a container and shelling into it:

```
docker run -it --rm thedatabaseme/awx-ee /bin/bash
```

You can check for the installed collections and versions then:

```
ansible-galaxy collection list
```

# Ansible Collections included in this image

The following collections are included in this EE image. I plan to pin
the versions of them to give more stability to this build:

```
awx.awx
azure.azcollection
amazon.aws
theforeman.foreman
google.cloud
openstack.cloud
community.general
community.vmware
community.docker
ovirt.ovirt
kubernetes.core
ansible.posix
ansible.windows
redhatinsights.insights
```

# Disclaimer


Most of code I (re)used from the official AWX EE project [here](https://github.com/ansible/awx-ee). So shoutout to them as well.

