# Satellite Monitor Docs
本仓库为整个卫星监控系统的相关文档以及各个配置的存放点.

## Quick Start(Ubuntu18.04 | 20.04)
clone所有仓库 & 安装所有服务
### 前置条件
- x86
- jdk17
- nodev16
  - pnpm@latest
- git
- mongodb

### 下载安装相关依赖
```bash
# 克隆对应的仓库并切换至master分支
git clone https://github.com/TachibanaKimika/satellite-monitor-server.git
git clone https://github.com/TachibanaKimika/satellite-monitor-web.git
git clone https://github.com/TachibanaKimika/satellite-monitor-client.git
git clone https://github.com/TachibanaKimika/satellite-monitor-docs.git

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
# 安装pnpm
npm install -g pnpm
```
### 启动服务
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

## 文件结构
- Architecture.drawio # 整体项目的架构图
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
  - exporter.md