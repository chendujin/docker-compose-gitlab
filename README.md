# 安装docker-compose-gitlab
# 安装步骤

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

## 3 克隆项目

```
git clone https://github.com/chendujin/docker-compose-gitlab.git
```

## 4 复制.env.example文件并重新命名为.env
根据自己实际情况更新.env文件里面的配置

```
# gitlab文件配置
GITLAB_CONFIG_DIR=./config
GITLAB_DATA_DIR=./data
GITLAB_LOGS_DIR=./logs
GITLAB_HOSTNAME=domain.com

# gitlab email配置
GITLAB_EXTERNAL_URL='http://domain.com'
GITLAB_RAILS_TIME_ZONE='PRC'
GITLAB_RAILS_SMTP_ENABLE=true
GITLAB_RAILS_SMTP_ADDRESS="smtp.qq.com"
GITLAB_RAILS_SMTP_PORT=465
GITLAB_RAILS_SMTP_USER_NAME="xxxxxx@qq.com"
GITLAB_RAILS_SMTP_PASSWORD="smtp-password"
GITLAB_RAILS_SMTP_AUTHENTICATION="login"
GITLAB_RAILS_SMTP_ENABLE_STARTTLS_AUTO=true
GITLAB_RAILS_SMTP_TLS=true
GITLAB_RAILS_GITLAB_EMAIL_FROM="xxxxxx@qq.com"
GITLAB_RAILS_GITLAB_SHELL_SSH_PORT=22
UNICORN_WORKER_PROCESSES=2
UNICORN_WORKER_TIMEOUT=60
SIDEKIQ_CONCURRENCY=5
POSTGRESQL_SHARED_BUFFERS="128MB"
POSTGRESQL_MAX_WORKER_PROCESSES=4

#端口映射
GITLAB_DOMAIN_PORT=8080
GITLAB_NGINX_PORT=8081
```

## 5 校验docker-compose.yml文件格式

```
docker-compose config
```

## 6 启动gitlab并观察日志

```
docker-compose up -d && docker-compose logs -f
```

## 7 访问gitlab

```
http://localhost:8080
```

## 8 docker-compose 常用命令

```
docker-compose up -d gitlab              构建建启动gitlab容器
docker-compose exec gitlab bash          登录到gitlab容器中
docker-compose down                      删除所有gitlab容器,镜像
docker-compose ps                        显示所有容器
docker-compose restart gitlab            重新启动gitlab容器
docker-compose build gitlab              构建镜像 。        
docker-compose build --no-cache gitlab   不带缓存的构建。
docker-compose logs  gitlab              查看gitlab的日志 
docker-compose logs -f gitlab            查看gitlab的实时日志
docker-compose config  -q                验证（docker-compose.yml）文件配置，当配置正确时，不输出任何内容，当文件配置错误，输出错误信息。 
docker-compose events --json gitlab      以json的形式输出gitlab的docker日志
docker-compose pause gitlab              暂停gitlab容器
docker-compose unpause gitlab            恢复gitlab容器
docker-compose stop gitlab               停止gitlab容器
docker-compose rm gitlab                 删除容器（删除前必须关闭容器）
docker-compose start gitlab              启动ngitlab容器
docker stats                             查看所有容器的内存、CPU状态
docker inspect -f '{{.Name}} - {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps -aq) 查看所有容器的内网IP地址
```