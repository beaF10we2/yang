docker

常见命令。

```
查看磁盘
docker system df

清理磁盘
清理镜像，卷
docker system prune -a 
docker volume prune 

查看基本信息
docker info

启动环境
docker-compose build
docker-compose up -d

关闭容器
docker stop id

进入容器
docker exec -it id /bin/bash
```

