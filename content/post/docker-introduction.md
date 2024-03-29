+++
author = "roiwk"
title = "Docker 入门"
description = "docker入门"
date = "2018-12-07"
keywords = [
    "docker",
]
tags = [
    "docker",
    "primer",
]
categories = [
    "docker",
    "primer",
]
draft = false
+++

<p>
 <a href="https://gitee.com/roiwk/docker_sharing">
    <img src="https://img.shields.io/badge/roiwk-docker_sharing-C71D23?logo=gitee" alt="gitee" title="roiwk/docker_sharing"/>
  </a>
</p>

# Docker 入门

![Docker](/images/docker.jpg)

----------------------------

# Docker

## 一. 是什么

### 1.Docker概念与简要历史
> Docker 是一个开源的应用容器引擎，你可以将其理解为一个轻量级的虚拟机，
> 开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上。

> Docker 最初是 dotCloud 公司创始人 Solomon Hykes 在法国期间发起的一个公司内部项目，它是基于 dotCloud 公司多年云服务技术的一次革新，
> 并于 2013 年 3 月以 Apache 2.0 授权协议开源，主要项目代码在 GitHub 上进行维护。Docker 项目后来还加入了 Linux 基金会，并成立推动 开放容器联盟（OCI）。

> Docker 自开源后受到广泛的关注和讨论，至今其 GitHub 项目已经超过 4 万 6 千个星标和一万多个 fork。
> 甚至由于 Docker 项目的火爆，在 2013 年底，dotCloud 公司决定改名为Docker。
> Docker 最初是在 Ubuntu 12.04 上开发实现的；Red Hat 则从 RHEL 6.5 开始对Docker 进行支持；Google 也在其 PaaS 产品中广泛应用 Docker。

> Docker 使用 Google 公司推出的 Go 语言 进行开发实现，
> 基于 Linux 内核的cgroup，namespace，以及 AUFS 类的 Union FS 等技术，对进程进行封装隔离，属于 操作系统层面的虚拟化技术。
> `由于隔离的进程独立于宿主和其它的隔离的进程，因此也称其为容器。`
> 最初实现是基于 LXC，从 0.7 版本以后开始去除 LXC，转而使用自行开发的libcontainer，从 1.11 开始，则进一步演进为使用 runC 和 containerd。

> Docker 在容器的基础上，进行了进一步的封装，从文件系统、网络互联到进程隔离等等，极大的简化了容器的创建和维护。
> 使得 Docker 技术比虚拟机技术更为轻便、快捷。

### 2.与传统虚拟方式的不同
> 传统虚拟机技术是虚拟出一套硬件后，在其上`运行一个完整操作系统，在该系统上再运行所需应用进程`；
> 而容器内的应用进程直接`运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。`因此容器要比传统虚拟机更为轻便。

![传统虚拟化](/images/docker-virtualization.png "每个虚拟化应用程序不仅包括应用程序[可能只有10几MB]和必要的二进制文件和库，而且还包括整个客户操作系统[可能有10几GB].")

![Docker](/images/docker-level.png "Docker引擎容器只包含应用程序及其依赖项。它在主机操作系统的用户空间中作为一个独立的进程运行，与其他容器共享内核。因此，它具有vm的资源隔离和分配优点，但可移植性和效率更高。")

-----------------------------

## 二. 为什么

### 1.使用Docker的原因
> 作为一种新兴的虚拟化方式，Docker 跟传统的虚拟化方式相比具有众多的优势。

1> **更高效的利用系统资源**
> 由于容器不需要进行硬件虚拟以及运行完整操作系统等额外开销，Docker 对系统资源的利用率更高。
> 无论是应用执行速度、内存损耗或者文件存储速度，都要比传统虚拟机技术更高效。
> 因此，相比虚拟机技术，一个相同配置的主机，往往可以运行更多数量的应用。

2> **更快速的启动时间**
> 传统的虚拟机技术启动应用服务往往需要数分钟，而 Docker 容器应用，由于直接运行于宿主内核，无需启动完整的操作系统，因此可以做到秒级、甚至毫秒级的启动时间。
> 大大的节约了开发、测试、部署的时间。

3> **一致的运行环境**
> 开发过程中一个常见的问题是环境一致性问题。由于开发环境、测试环境、生产环境不一致，导致有些 bug 并未在开发过程中被发现。
> 而 Docker 的镜像提供了除内核外完整的运行时环境，确保了应用运行环境一致性，从而不会再出现 「这段代码在我机器上没问题啊」 这类问题。

4> **持续交付和部署**
> 对开发和运维（DevOps）人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。
> 使用 Docker 可以通过定制应用镜像来实现持续集成、持续交付、部署。
> 开发人员可以通过 Dockerfile 来进行镜像构建，并结合持续集成(Continuous Integration) 系统进行集成测试，
> 而运维人员则可以直接在生产环境中快速部署该镜像，甚至结合 持续部署(Continuous Delivery/Deployment) 系统进行自动部署。
> 而且使用 Dockerfile 使镜像构建透明化，不仅仅开发团队可以理解应用运行环境，也方便运维团队理解应用运行所需条件，帮助更好的生产环境中部署该镜像。

5> **更轻松的迁移**
> 由于 Docker 确保了执行环境的一致性，使得应用的迁移更加容易。
> Docker 可以在很多平台上运行，无论是物理机、虚拟机、公有云、私有云，甚至是笔记本，其运行结果是一致的。
> 因此用户可以很轻易的将在一个平台上运行的应用，迁移到另一个平台上，而不用担心运行环境的变化导致应用无法正常运行的情况。

6> **更轻松的维护和扩展**
> Docker 使用的分层存储以及镜像的技术，使得应用重复部分的复用更为容易，也使得应用的维护更新更加简单，基于基础镜像进一步扩展镜像也变得非常简单。
> 此外，Docker 团队同各个开源项目团队一起维护了一大批高质量的 官方镜像，既可以直接在生产环境使用，又可以作为基础进一步定制，大大的降低了应用服务的镜像制作成本。

7> **对比传统虚拟机总结**

| 特性 | 容器 | 虚拟机 |
| --- | --- | --- |
| 启动 | 秒级 | 分钟级 |
| 硬件使用 | 一般为MB | 一般为GB |
| 性能 | 接近原生 | 弱于 |
| 系统支持量 | 单机支持上千个容器 | 一般几十个 |



### 2.用途

1> **提供一次性的环境。**
> 比如，本地测试他人的软件、持续集成的时候提供单元测试和构建的环境。

2> **提供弹性的云服务。**
> 因为 Docker 容器可以随开随关，很适合动态扩容和缩容。

3> **组建微服务架构。**
> 通过多个容器，一台机器可以跑多个服务，因此在本机就可以模拟出微服务架构。


-----------------------

## 三. 怎么做


### 1.基本概念

1> **镜像**
*  *镜像就是一个只读的模板。*
> 例如：一个镜像可以包含一个完整的 ubuntu 操作系统环境，里面仅安装了 Apache 或用户需要的其它应用程序。
*  镜像可以用来创建 Docker 容器。
> Docker 提供了一个很简单的机制来创建镜像或者更新现有的镜像，用户甚至可以直接从其他人那里下载一个已经做好的镜像来直接使用。

2> **容器**
* *Docker 利用容器来运行应用。*
> 容器是从镜像创建的运行实例。它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台。
> 可以把容器看做是一个简易版的 Linux 环境（包括root用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。

3> **仓库**
* *仓库是集中存放镜像文件的场所。*
> 有时候会把仓库和仓库注册服务器（Registry）混为一谈，并不严格区分。实际上，仓库注册服务器上往往存放着多个仓库，每个仓库中又包含了多个镜像，每个镜像有不同的标签（tag）。
* 仓库分为公开仓库（Public）和私有仓库（Private）两种形式。
* 最大的公开仓库是 [Docker Hub](https://hub.docker.com/)，存放了数量庞大的镜像供用户下载。



### 2.快速入门

#### 安装下载
[win10/mac 下载](https://www.docker.com/get-started)
[win10以下版本下载 docker-tool](https://docs.docker.com/toolbox/toolbox_install_windows/)

#### 实战nginx容器搭建
*要求：配置和站点文件不放进容器（方便管理）*
[官方仓库](https://hub.docker.com/)


![Docker](/images/docker-flow.png)
```flowchart
sart=>start: 开始:>https://hub.docker.com/_/nginx/[blank]
end=>end: 结束:>https://hub.docker.com/_/nginx/[blank]
io_input=>inputoutput: 搭建后销毁nginx
op_pull=>operation: 拉取镜像(docker pull)
op_run=>operation: 运行容器(docker run)
op_stop=>operation: 停止容器(docker stop)
op_destory=>operation: 销毁容器(docker rm)
op_rm=>operation: 删除镜像(docker rmi)
io_service=>inputoutput: 完成-搭建后销毁
sub_params=>subroutine: 进入容器(docker exec)

op_stop=>operation: 容器关闭状态
cond_stop=>condition: 是否关闭容器?
sub_stop=>subroutine: 关闭容器(docker stop)

sart->io_input->op_pull->op_run->sub_params->op_destory->op_rm->io_service

cond_stop(yes)->sub_stop->op_stop
cond_stop(no)->io_service->end

```


- 创建需要挂载的文件夹目录结构

| 文件、目录名| 说明 |
| :--- | :--- |
| -docker | 将挂载到容器中 |
| ---nginx | nginx容器相关文件目录 |
| -----conf | 配置目录 |
| -------nginx.conf | 配置文件 |
| -----www | nginx站点目录 |
| -------index.html | 主页文件 |


* 拉取镜像

```shell
docker pull nginx:1.15.7
```

* 运行容器

```shell
docker run --name nginx1 -v /c/User/share/docker/nginx/www:/usr/share/nginx/html:rw -v /c/User/share/docker/nginx/conf/nginx.conf:/etc/nginx/nginx.conf:ro -p 8000:80 -d nginx:1.15.7
```
> 注：挂载目录尽量使用绝对路径

* 进入容器

```shell
docker exec -it nginx1 bash
```

* 停止容器

```shell
docker stop nginx1
```

* 销毁容器

```shell
docker rm nginx1
```

* 销毁镜像

```shell
docker rmi nginx:1.15.7
```

### 3.深入与提高
#### 1> Dockerfile文件
> Dockerfile 是一个文本文件，其内包含了一条条的指令(Instruction)，每一条指令构建一层，因此每一条指令的内容，就是描述该层应当如何构建。


#### 2> yml文件
> 下面三剑客中docker-compose的编排文件。用于快速配置和管理一组服务容器（项目）。

#### 3> Docker三剑客

##### Docker Compose
> 负责快速的部署分布式应用。
> Compose  定位是 「定义和运行多个 Docker 容器的应用（Defining and running multi-container Docker applications）」

##### Docker Machine
> Docker Machine 是 Docker 官方编排（Orchestration）项目
> 负责在多种平台上快速安装 Docker 环境。

![docker-machine](/images/docker-machine.png)



##### Docker Swarm
> 提供 Docker 容器集群服务，是 Docker 官方对容器云生态进行支持的核心方案。

![管理节点与工作节点的关系](/images/docker-swarm.png)

-----------------------
