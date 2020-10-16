---


layout: post
title: 'Ubuntu18.04中安装带NVIDIA的Docker环境'
tags: [code]
---

## 环境准备

1. 卸载旧版本的Docker

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

2. 安装需要的依赖包

```bash
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

3. 加入 Docker 官方的 GPG Key 到本地系统中

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# 验证是否拥有指定的密钥
sudo apt-key fingerprint 0EBFCD88
```

4. 加入 Docker 官方源到 APT 配置文件中

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

## 安装Docker

1. 更新apt程序包索引，

```bash
sudo apt update
```

2. 安装指定版本的Docker

```bash
# 查询仓库中可用的Dokcer版本
sudo apt-cache madison docker-ce

# 安装指定的版本的Docker Engine 和容器 19.03.13~3-0~ubuntu
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

3. 测试Docker是否安装成功

```bash
sudo docker run --rm hello-world
```

## 安装 NVIDIA Container Toolkit

1. 配置repo并安装

```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list


sudo apt-get update

sudo apt-get install nvidia-container-toolkit


sudo systemctl restart docker
```

2. 测试 NVIDIA Container Toolkit

```bash
sudo docker run --gpus all --rm nvidia/cuda nvidia-smi
```

## 设定用户权限

因为在安装 Docker 是，自动在系统中建了一个名叫: docker 的组（group），该组的用户有权限执行 Docker 相关的命令。所以我们只需要把当前用户加入到 docker 组中即可。执行以下命令：

```bash
sudo usermod -aG docker zhaoliu
```

