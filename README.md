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
### 2、
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
# go 交叉编译
```
set GOOS=linux
set GOARCH=arm64
go build main.go
```
