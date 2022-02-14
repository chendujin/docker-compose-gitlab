# 安装docker-compose-gitlab
# 准备

## 1 安装docker

```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

并根据需要配置国内源。

## 2 下载docker-compose

参考[文档](https://docs.docker.com/compose/install/).

```
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```