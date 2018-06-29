https://wenku.baidu.com/view/33fc29e17375a417876f8f92.html?from=search
https://yeasy.gitbooks.io/docker_practice/content/introduction/what.html
http://www.runoob.com/docker/docker-container-connection.html

win10
https://www.cnblogs.com/studyzy/p/6113221.html

	* Docker简介

		* 1. 什么是Docker

			* Docker 是一个开源的应用容器引擎，
			* Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。
			* 容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app），更重要的是容器性能开销极低。
		* 2.Docker与虚拟机的区别

        物理主机         虚拟机Docker容器特性Docker虚拟机启动秒级分钟级硬盘使用一般为MB一般为GB性能接近原生弱于系统支持量单机支持上千个容器一般几十个
	* 3.为什么用Docker

		* 更高效的利用系统资源
		* 更快速的启动时间
		* 一致的运行环境
		* 自动化测试和持续集成、发布
		* 更轻松的迁移
		* 更轻松的维护和扩展


	* Docker的一些概念

		* 镜像（image）

			* Docker镜像就是一个只读的模板文件，只有通过镜像文件才能创建容器
			* 在实际开发中，一个image文件往往通过继承另一个image文件，加上一些个性化设置生成而成，例如，可以在Ubuntu的image基础上，往里面加入tensorflow库等其他依赖库，形成自己的image
			* Docker提供了一个简单的机制来创建镜像或者更新现有镜像，不同机器的image文件是可以相互通用的，一般来说我们应尽量使用其他人制作好的image文件，或是基于其他人的image文件进行加工。
		* 容器（container）

			* Docker容器是从镜像创建的运行实例，可以被启动，开始，停止，删除。也就是说，一旦容器生成，就会同时存在
			* Docker中的容器和文件夹很类似，一个Docker容器包含了所有的某个应用运行所需的环境，并且每个容器都是相互隔离的，保证安全的平台
		* 仓库（registry）

			* 仓库是Docker集中放镜像文件的场所，分为公开仓库和私有仓库
			* 最大的公开仓库是Docker Hub(https://hub.docker.com/)，存放了数量庞大的镜像供用户下载，由于某些原因，国内一些云服务提供厂商提供了针对Docker Hub的镜像服务，常见的有阿里云加速器，DaoCloud加速器等
			* 私有Docker镜像是用户在本地搭建的私有化Docker Registry
			* 用户创建自己的镜像后，可以通过push和pull在仓库中进行上传或下载
	* 安装

		* 可以参考Docker官网(https://docs.docker.com/install/)提供的安装文档
	* 具体操作
	* 镜像
	* 获取镜像： docker pull ubuntu:16.04

		* 从官方仓库（Docker Hub）中拉取一个ubuntu:16.04
	* 列出本地镜像：docker images
	* 通过镜像创建容器：docker run -it -rm ubuntu:16.04 /bash/bin

		* docker run 就是运行容器的命令，-it：这是两个参数，一个是 -i：交互式操作，一个是 -t 终端。我们这里打算进入 bash 执行一些命令并查看返回结果，因此我们需要交互式终端。
		* --rm：这个参数是说容器退出后随之将其删除。默认情况下，为了排障需求，退出的容器并不会立即删除，除非手动 docker rm。我们这里只是随便执行个命令，看看结果，不需要排障和保留结果，因此使用 --rm 可以避免浪费空间。
		* ubuntu:16.04：这是指用 ubuntu:16.04 镜像为基础来启动容器。
		* bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 bash。
		* 最后通过exit退出容器
	* 创建镜像：

		* 1、通过进入容器修改镜像：docker commit -m "message" -a "author" [容器ID] [新的镜像名称]
		* 慎用docker commit命令
		* 2、Dockerfile创建镜像：FROM: 指令告诉Docker使用哪个镜像作为基础，RUN会在创建中运行，比如安装一个软件包等。Dockerfile创建好后，使用docker build [OPTIONS] [PATH]

	* 存储和载入镜像

		* 存储镜像：docker save -o ubuntu_14.04.tar ubuntu:14.04
		* 载入镜像：docker load --input ubuntu_14.04.tar
	* 容器
	* 启动容器

		* 1、新建并启动：docker run -it -rm ubuntu:16.04 /bash/bin
		* 2、启动已终止的容器：先通过docker ps查看容器信息，之后通过docker start [ID]启动以终止的容器
	* 守护态运行

		* 很多时候需要让Docker在后台运行，可以通过-d参数实现docker run -it -d ubuntu:16.04 /bin/sh -C [COMMOND]
		* 通过 docker ps查看容器信息，通过 docker logs获取容器输出信息
	* 终止容器：docker stop
	* 重启容器：docker restart
	* 进入容器：docker exec -it [ID] /bin/bash
	* 导入导出容器：

		* 导出为镜像：docker commit [ID] [IMAGE NAME]
		* 导出为容器快照：docker export -o [FILE NAME] [ID] 
		* 导入容器快照：docker import [FILE NAME] [IMAGE NAME]
	* 删除容器：docker rm
	* 
	* Docker与主机之间的通讯：
	* 数据传输：docker cp [主机文件路径] [容器ID]:[容器路径]
	* 目录挂载：docker run -v [主机文件路径]:[镜像路径] [镜像名称]
	* 端口映射：docker run -p 8000
	* 图像显示：docker run -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY


