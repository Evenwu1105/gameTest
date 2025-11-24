# 镜像源：[docker.io/jenkins/jenkins:lts-jdk17 - 镜像下载 | docker.io](https://docker.aityp.com/image/docker.io/jenkins/jenkins:lts-jdk17)
# 启动命令：# 简单启动（映射8080端口，方便浏览器访问） 
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/jenkins/jenkins:lts-jdk17
# 打开网页：localhost:8080

打开 Windows 终端，进入 Jenkins 容器命令行：

```bash
docker exec -it jenkins /bin/bash
```

```bash
exit  # 输入后按回车，会回到 Windows 终端（提示符变成 C:\Users\Evenwu> 之类）
```
