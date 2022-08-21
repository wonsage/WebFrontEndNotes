容器 比 虚拟机 (VM) 更加接近原生，性能更好，
容器解决了环境不一致的问题。
Docker 是容器技术中的一个优秀引擎。
镜像 Image
提供容器运行时所需的程序、库、资源、配置等文件，包含了配置参数（），不包含任何动态数据。镜像的内容在构建之后不会改变。只读，由 dockfile 创建。
容器 Container
镜像 + 读写层。容器与容器、容器与宿主机之间都是互相隔离的。
仓库 Repository
存放镜像文件的地方。像git那样可以pull、push

#### 前端应用场景
1. 快速部署
2. 隔离应用
3. 提高开发效率
4. 版本控制
5. DevOps流程
#### 常用命令
##### 创建
- `run`：Run a command in a new container 创建容器并启动
	- `-it`：i terminal 提供交互式的终端工具
		- `-i`：容器保持标准输入流对容器开放,即使容器没有终端连接
		- `-t`：为容器分配一个虚拟终端
	- `-v [hostDir]:[containerDir]`：volume 挂载宿主机的文件目录到容器，容器中对该目录文件的修改会影响宿主机下的该目录。
	- `-p [hostPort]:[containerPort]`：将容器某端口映射到宿主机的某端口使用
	- `-d`：以守护进程的方式让镜像容器在后台持续运行
	- `--name [containerName]`：指定容器的名称，指代容器ID
	- `-privileged`：让容器的用户在容器内能获取完全root权限
- `create`：创建容器
- `exec`：进入容器操作执行命令
##### 管理
- `stop`：停止一个正在运行的容器
- `start`：启动一个已停止的容器
- `restart`：重启一个正在运行的容器
- `rm [containerName/containerId]`：删除一个已停止的容器
- `rmi [imageName/imageId]`：删除一个当前没有容器使用的镜像
- `ps`：查看**运行中**的容器
	- `-a`：all，查看所有容器
##### 构建镜像
- `commit`
	`docker commit <container_id> <namespace>/<image_name>:<tag_name>`
- `tag`
- `push [imageName]:[version]`
- `pull`：从远端拉取镜像
#### 
### 应用Docker
#### Dockerfile
Dockerfile 是一个由命令和参数构成的脚本。一般包括四部分：
- 基础镜像信息
- 维护者信息
- 镜像操作指令
- 容器启动时执行指令
### docker-compose
批量执行 docker，多容器集成
- service 服务：
- project 项目：
#### docker-compose.yml