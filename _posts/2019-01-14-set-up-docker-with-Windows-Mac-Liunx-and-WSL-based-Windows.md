---
layout: post
title: Docker dev environment setup for Windows/Mac/Liux/WSL based Windows
date: 2019-01-14 13:59 +1000
description: Docker Dev Environment set up# Add post description (optional)
img: docker.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Docker]
---

With the development of cloud computing technology and the docker, now we containerize the application, which makes the whole process for devlopment and deployment change.

It is also making our life much easier and save quite a lot time for us as our environment from dev to production can be the same with docker now.

So we should use docker to do the development, and embrace the docker.

Today, I will describe the basic process about how to setup the docker dev environment for the three OS. Especially Windows.

### Introduction
Our aim is to install and make it work with `docker` and `docker-compose`, which will be enought for our daily development.

### Mac
Download the docker-ce from official website: [download link](https://docs.docker.com/docker-for-mac/install/)
Then click install, restart computer, and login your docker hub account, everything done.

### Linux
We use Ubuntu18.04 as an example.
1. install the docker:
```shell
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
```
2. install docker-compose
```shell
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
Then all done
You can check it with command: `docker info` and `docker-compose -v`

### Windows with WSL
1. Install docker-ce in Windows, you will need to be Windows Pro Version, [download link](https://docs.docker.com/docker-for-windows/install/)
2. Click and Install it
3. Set the Windows docker
    - In settings => general => check "expose damon on tcp..."
    - In settings => Shared Drive => check the drive you have
4. Install Ubuntu 18.04 as the subsystem, which need to 
    - enable the subsystem feature first
    - install Ubunut 18.04 in Windows App Store
5. Install Docker and Docker-compose on Ubuntu 18.04, as described above
6. Run `echo "export DOCKER_HOST=tcp://localhost:2375" >> ~/.bashrc && source ~/.bashrc`
7. Change Windows Mount Volume
    - `sudo nano /etc/wsl.conf`
    - then put the below info in
        ```shell
        # Now make it look like this and save the file when you're done:
        [automount]
        root = /
        options = "metadata"
        ```
8. Restart the computer, and open the Ubuntu 18.04, you should see the directory structure like: `/c/`, not `/mnt/c` anymore
9. Then congratutions, it works, we can start to use it now.

The key point here it that:
- Windows and Linux docker should work together, so you need to install both of them.
- And the directory structure for the Windows SubSystem is not suitable for docker to check the volume, we should change it.

### Source
- [how to make windows and wsl work together](https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly)
- [Linux install docker-compose](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04)
- [Linux install docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)