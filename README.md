## Docker container with fli4l Buildroot
 
 This is a docker implementation of all required tools to build fli4l from 
 scratch.

 For more information please refer to [Official website](http://www.fli4l.de/)
 or [Support forum](https://forum.nettworks.org)

### 1. Install docker

 This instruction works for a <b>Centos7</b> docker host. Other distributions 
 may need some adjustments.

```shell
sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/7/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
...
sudo yum install docker-engine -y
...
sudo systemctl enable docker.service
...
sudo systemctl start docker.service
```

### 2. Build/Use the Container

You now have two options: 
- Build from scratch or 
- Pull the ready-made image from DockerHub. 

#### 2a Image from Docker Hub

```shell
sudo docker pull starwarsfan/fli4l-buildroot-container
```

#### 2b Build from scratch

##### Pull repo from github

```shell
sudo git clone https://github.com/starwarsfan/fli4l-buildroot-container.git
cd fli4l-buildroot-container
```

##### Build image

```shell
sudo docker build -t starwarsfan/fli4l-buildroot-container:latest .
```

### 3. Starting docker container

```shell
sudo docker run \
    --name fli4l-buildroot-container \
    -d \
    starwarsfan/fli4l-buildroot-container:latest
```

#### 3.a Mount volume or folder for svn checkout

With the additional run parameter _-v <host-folder>:/data/work/_ you can mount 
a folder on the docker host which contains the the svn checkout outside of the
container. So the run command may look like the following example:

```shell
sudo docker run \
    --name fli4l-buildroot-container \
    -v /data/svn-checkout/:/data/work/ ...
```

### 5. Useful commands

Check running / stopped container:

```shell
sudo docker ps -a
```

Stop the container

```shell
sudo docker stop fli4l-3.10-buildroot-container
```

Start the container

```shell
sudo docker start fli4l-3.10-buildroot-container
```

Get logs from container

```shell
sudo docker logs -f fli4l-3.10-buildroot-container
```

Open cmdline inside of container

```shell
sudo docker exec -i -t fli4l-3.10-buildroot-container /bin/bash
```

