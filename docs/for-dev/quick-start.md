# 快速开始
本文将介绍基础开发环境的搭建(windows10)以及如何将各个项目跑起来

## 安装基础服务
### 基本依赖
#### Nodejs^16
[点击下载](https://nodejs.org/dist/v16.14.0/node-v16.14.0-x64.msi)
##### pnpm
运行以下命令等待安装完成即可
```bash
npm i -g pnpm@latest
```

下载完成后运行安装即可
#### JKD17
[点击下载](https://download.oracle.com/java/17/archive/jdk-17.0.6_windows-x64_bin.msi)

下载完成后直接运行安装即可
#### git
[点击下载](https://github.com/git-for-windows/git/releases/download/v2.39.1.windows.1/Git-2.39.1-64-bit.exe)

下载完成后直接运行安装即可
### Prometheus
```bash
# 下载并解压对应的服务
# prometheus版本为2.41.0
wget https://github.com/prometheus/prometheus/releases/download/v2.40.7/prometheus-2.40.7.linux-amd64.tar.gz
tar -zxvf /prometheus-2.40.7.linux-amd64.tar.gz
# pushgateway版本为1.5.1
wget https://github.com/prometheus/pushgateway/releases/download/v1.5.1/pushgateway-1.5.1.linux-amd64.tar.gz
tar -zxvf /pushgateway-1.5.1.linux-amd64.tar.gz
# alert manager版本为0.25.0
wget https://github.com/prometheus/alertmanager/releases/download/v0.25.0/alertmanager-0.25.0.linux-amd64.tar.gz
tar -zxvf /alertmanager-0.25.0.linux-amd64.tar.gz
# grafana版本为9.3.2(oss版本)
sudo apt-get install -y adduser libfontconfig1
wget https://dl.grafana.com/oss/release/grafana_9.3.2_amd64.deb
sudo dpkg -i grafana_9.3.2_amd64.deb
```
### MongoDB
下载`6.x.x`版本的MongoDB即可

[点击下载](https://repo.mongodb.org/yum/amazon/2/mongodb-org/6.0/x86_64/RPMS/mongodb-org-server-6.0.4-1.amzn2.x86_64.rpm)

下载完成后运行安装即可
## 下载各个代码仓库
```bash
# 克隆对应的仓库并切换至master分支
git clone -b dev https://github.com/TachibanaKimika/satellite-monitor-server.git
git clone -b dev https://github.com/TachibanaKimika/satellite-monitor-web.git
git clone -b dev https://github.com/TachibanaKimika/satellite-monitor-client.git
git clone -b dev https://github.com/TachibanaKimika/satellite-monitor-docs.git

```
## 启动各个服务
```bash
# 将satellite-monitor-docs/prom/config中的配置文件复制到对应的地方
# 略

# 进入prometheus文件夹启动服务
./prometheus.exe --web.enable-admin-api

# 进入pushgateway文件夹启动服务
./pushgateway

# alertmanager文件夹
./alertmanager

# grafana参照linux启动配置 https://grafana.com/docs/grafana/v8.5/installation/debian/#2-start-the-server
# 略

# 进入satellite-monitor-server 目录
./script/start.sh

# 进入satellite-monitor-web 目录
pnpm start:main
```

<!-- # 文件结构
- server # 服务端(包括SpringBoot和Nodejs两个后端)的项目文档
  - apis.md # api文档(postman导出markdown)
  - docs.md # 相关架构文档
  - db.md # 数据库设计文档
- frontend # 前端
  - index.md # 前端架构文档
- prom # prometheus以及相关生态
  - config # 各个配置文件的存放点
  - promthues.md
  - alertmanager.md
  - exporter.md -->