# Google Cloud

## Computer Engine

Click on create a new instance, once in the configuration panel, build your instance.

Once the instance is builded, connect with SSH (via the interface) or via SSH terminal.

## Creation of a new user
```bash
adduser newuser
ls -l /home/newuser
```

**_If the root rights are needed_**

```bash
su root _command_
```

- If the password need to be redefined :

```bash
passwd concernedUser
```

**For security purpose, be sure to connect with this user instead of the default one !**

## Git

```bash
apt-get install git -y
git --version # For verification purpose.
```

### Nginx

```bash
apt-get update -y && apt-get upgrade -y
apt-get install -y nginx
```

- Open the ipadress/ and check that Nginx homepage is visible.

### Docker

```bash
sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
```

- Check for the fingerprint (9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88) :

```bash
apt-key fingerprint 0EBFCD88
```

- Add the repository and install Docker-CE

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"
apt-get update -y && apt-get upgrade -y
apt-get install docker-ce -y
```

- Check the installation :

```bash
docker run hello-world
```

You should see something similar :

```bash
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
5b0f327be733: Pull complete
Digest: sha256:07d5f7800dfe37b8c2196c7b1c524c33808ce2e0f74e7aa00e603295ca9a0972
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
```

### Docker-Compose

[Documentation]('https://docs.docker.com/compose/install/')

### Docker Swarm

```bash
docker -v
docker swarm init
```

**_The Docker compose version is defined in the [Docker repository](https://github.com/docker/compose/releases), be sure top use the latest_**

**_For simplicity, the Swarm mode is activated in order to achieve the service approach_**

### Symfony project using Docker-Compose

First, we need to ...
