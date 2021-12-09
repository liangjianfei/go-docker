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
