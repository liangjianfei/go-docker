# go-docker
go 项目 docker 化

### 代码在master分支

#### 构建gin-api image 在api-app目录下执行下面命令

```docker
docker build -t gin-api .
```

#### 构建gin-kafka image 在kafka-app目录下执行下面命令

```docker
docker build -t gin-kafka .
```

#### 使用docker-compose 启动容器

```docker
docker-compose up -d
```

# Dockerfile 自定义镜像基础
### 1、FROM
制定基础镜像（必须有的指令，并且必须是第一条指令）
### 2、WORKDIR
格式为```WORKDIR<工作目录路径>
使用WORKDIR指令可以来指定工作目录（或者称为当前目录），以后各层的当前目录就被改为指定的目录，如果目录不存在，WORKDIR会帮你建立目录
### 3、COPY
格式
```
COPY <源路径>... <目标路径>
COPY ["<源路径1>",... "<目标路径>"]
```
COPY指令将从构建上下文目录中<源路径>的文件/目录复制到新的一层的镜像内的<目标路径>位置
### 4、RUN
用于执行命令行命令
格式：
```
RUN <命令>
```
### 5、EXPOSE
格式为：
```
EXPOSE <端口1>[<端口2>...]
```
EXPOSE 指令是声明运行时容器提供服务端口，这只是一个声明，在运行时并不会因为这个声明应用就会开启这个端口的服务
##### 在 Dockerfile 中写入这样的声明有两个好处

* 帮助镜像使用者理解这个镜像服务的守护端口，以方便配置映射
* 运行时使用随机端口映射时，也就是 docker run -P 时，会自动随机映射 EXPOSE 的端口

## 容器关联
将 ```Golang``` 容器和 ```Mysql``` 容器关联起来
* 增加命令 ```--link mysql:mysql``` 让 Golang 容器与 Mysql 容器互联；通过 ```--link```，可以在容器内直接使用其关联的容器别名进行访问，而不通过IP，但是```--link```只能解决单机容器间的关联，在分布式多机的情况下，需要通过别的方式进行连接
```
docker run --link mysql:mysql -p 8000:8000 gin-blog-docker
```

# Docker Compose
##### 除了像上面一样使用--link的方式来关联两个容器之外，我们还可以使用Docker Compose来定义和运行多个容器。Compose是用于定义和运行多容器 Docker 应用程序的工具。通过 Compose，你可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务。

#### 使用Compose基本上是一个三步过程：
1. 使用Dockerfile定义你的应用环境以便可以在任何地方复制。
2. 定义组成应用程序的服务，docker-compose.yml 以便它们可以在隔离的环境中一起运行。
3. 执行 docker-compose up命令来启动并运行整个应用程序。

# go 交叉编译
```
set GOOS=linux
set GOARCH=arm64
go build main.go
```
