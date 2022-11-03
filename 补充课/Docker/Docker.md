## 官方文档
[Docker Docs](https://docs.docker.com/get-started/overview/)
## 大致说明
容器技术是Linux中存在已久的技术，Docker是容器技术一个流行的实现。![vm-vs-docker-architecture1.png](https://cdn.nlark.com/yuque/0/2022/png/21954736/1657165745233-76ca5259-af4b-4a16-bcec-2ab6764ece30.png#clientId=u3c9d68eb-de3f-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u14cab0de&margin=%5Bobject%20Object%5D&name=vm-vs-docker-architecture1.png&originHeight=596&originWidth=1043&originalType=binary&ratio=1&rotation=0&showTitle=true&size=86097&status=done&style=none&taskId=u57f514f7-6d2c-40fc-a3b0-e53340383be&title=%E8%99%9A%E6%8B%9F%E6%9C%BA%E5%92%8CDocker%28%E5%AE%B9%E5%99%A8%E6%8A%80%E6%9C%AF%29%E7%9A%84%E5%AF%B9%E6%AF%94 "虚拟机和Docker(容器技术)的对比")
## 架构与概念
![architecture.svg](https://cdn.nlark.com/yuque/0/2022/svg/21954736/1657072407727-c2aa7e3f-2db1-4454-95d0-dc655aa7b811.svg#clientId=u3e3d35d5-608d-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u159fd1ac&margin=%5Bobject%20Object%5D&name=architecture.svg&originHeight=527&originWidth=1009&originalType=binary&ratio=1&rotation=0&showTitle=true&size=187350&status=done&style=none&taskId=u9ec74ea6-0056-4ab2-b6d8-93bce6b64a1&title=Docker%E6%9E%B6%E6%9E%84 "Docker架构")

### 镜像 Image
可以理解为一个便于分发的只读模板，用于创建容器。
### 容器 Container
宿主机下的沙盒独立进程，是镜像的可运行实例。各个容器间彼此独立。
### 源 Registry
分发镜像，比如Docker Hub。
### 主机 Host
### 客户端 Client
## CLI
### 镜像相关
#### 删除镜像`docker rmi [OPTIONS] <IMAGE> [IMAGE...]`

### `docker image <CMD>`管理镜像

- `docker image ls`镜像列表
- `docker image pull`拉取镜像
- `docker image push`推送镜像
- 查看镜像列表`docker images`
- 从源搜索镜像`docker search <image_name>`
- 拉取镜像`docker pull <image_name>`
   - 指定版本`<image_name>:<version>`
- 删除镜像`docker rmi <image_id>`
   - 指定要删除镜像的标签`docker rmi <image_id>:<tag>`
   - 强制删除`docker rmi -f <image_id>`
- 构建镜像`docker build [OPTIONS] <PATH> | <URL>`
   - --tag/-t 打标签`docker build -t <tag_name>`
### 容器相关命令
#### 容器列表`ps [OPTIONS]`
OPTIONS
- 默认只显示正在运行的
- `-a`,`--all` 所有容器
- `-q`, `--quiet` 只显示容器ID
#### 从镜像创建容器并启动`run [<options>] <IMAGE> [CMD] [ARG...]`
OPTIONS
- `-d`,`--detach`后台运行容器（并打印这个容器的ID）
- `-p`,`--publish`发布容器端口到主机上，即可在主机上访问容器端口下的服务
e.g.`docker run -dp 80:80 starter`
- `-it`,-it参数：容器的 Shell 映射到当前的 Shell，然后你在本机窗口输入的命令，就会传入容器
- `--rm`退出后自动删除容器
#### 启动容器`start <container_name>:<tag> | <container_id>`
#### 在一个运行中的容器内执行命令`exec [<OPTIONS>] <CONTAINER> <CMD> [ARG...]`
#### 查看容器的输出`logs [<OPTIONS>] CONTAINER`
#### 在正在运行的容器和本机之间拷贝`cp [<CONTAINER>]:[PATH]`
#### 停止运行容器`docker stop <CONTAINER_ID>`
#### 终止容器`docker kill <CONTAINER>`
与`stop`的区别在于，`kill`向容器里面的主进程发出 SIGKILL 信号，应用程序会立即强行终止，正在进行中的操作会全部丢失，`stop`向容器里面的主进程发出 SIGTERM 信号，然后过一段时间再发出 SIGKILL 信号，应用程序收到 SIGTERM 信号以后，可以自行进行收尾清理工作，但也可以不理会这个信号。
#### 删除容器`docker rm [<OPTIONS>] <CONTAINER>`
默认只能删除非运行中的容器
OPTIONS

- `-f`,`--force`强制删除，如果是运行中的容器会先停止
#### 管理容器`docker container <CMD>`

- `run`同`docker run`
- `docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]`
- `start`同`docker start`
- `stop`同`docker stop`
## 镜像构建文件夹的组成
### Dockerfile
Dockerfile是将文件夹构建为镜像的指导文件，描述了镜像构建的步骤。
## Dockerfile指令
### FROM[🔗](https://docs.docker.com/engine/reference/builder/#from)
`FROM <image_name>`指明基础镜像
### COPY[🔗](https://docs.docker.com/engine/reference/builder/#run)
`COPY <src_url> <dest_url>`将源地址下的文件拷贝到目标地址下
### WORKDIR[🔗](https://docs.docker.com/engine/reference/builder/#workdir)
`WORKDIR <url>`进入路径
### CMD[🔗](https://docs.docker.com/engine/reference/builder/#cmd)
`CMD <command>`执行命令
