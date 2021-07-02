[TOC]

## Install Docker CE yum repository on our CentOS 7 operating system.
On online system
```
sudo yum install -y yum-utils
```
```
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

```
mkdir ~/docker
cd ~/docker
```
This is very important ！！！
```
yumdownloader --resolve docker-ce docker-ce-cli containerd.io
```
中间如果有下载的链接失败需要手动下载
```
wget https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-cli-20.10.7-3.el7.x86_64.rpm

wget https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-ce-rootless-extras-20.10.7-3.el7.x86_64.rpm

wget https://download.docker.com/linux/centos/7/x86_64/stable/Packages/docker-scan-plugin-0.8.0-3.el7.x86_64.rpm
```
```
tar cvzf ~/docker.tar.gz *
```

## On offline system
```
mkdir docker
tar xvf docker.tar.gz -C ~/docker
cd docker
##rpm -ivh --replacefiles --replacepkgs *.rpm
rpm -Uvh *.rpm --force --nodeps
systemctl enable docker.service
systemctl start docker.service
```

## make docker images
On online system
```
docker save jenkins/jenkins > ~/jenkins.tar
```

## On offline system load docker images
```
docker load < jenkins.tar
```


# Install docker compose on offline system
On online system
```
wget https://github.com/docker/compose/releases/download/1.24.0/docker-compose-Linux-x86_64
```
```
mv docker-compose-Linux-x86_64 docker-compose
```

On offline system
```
mv docker-compose /usr/local/bin/
chmod +x /usr/local/bin/docker-compose
```

# create docker network
```
docker network create docker_network
```