# 安装说明

## 1. 准备

- Chrome 浏览器

Tapdata 目前仅在 Google Chrome 浏览器上进行测试。我们建议使用 51.0.2704 或更高版本。

- Java 1.8

运行命令 `java -version` 是否服务器安装了 jdk_1.8
    
- MongoDB 3.6

运行安装了 MongoDB 3.6 或更高版本的服务器命令 `mongod --version` 

请务必保证 MongoDB 采用了副本集架构

请参考以下链接安装 Java 或 MongoDB ：

[Java 8+](https://www.oracle.com/technetwork/java/javase/downloads/index.html)

[MongoDB 3.6+](https://www.mongodb.com/download-center)



## 2. 安装 Cloud Tapdata

您可以访问我们的网站 [http://cloud.tapdata.io](http://cloud.tapdata.io) 登录并获取 Tapdata 云版的下载链接，该版本一次仅限于1个正在运行的作业。

您也可以联系我们获取无限制的作业版本。我们的邮箱是：**team@tapdata.io**

1. 下载 Tapdata 二进制文件后，转到该目录并执行以下命令：

```
tar -zxvf tapdata-agent-x.x.x-xxxx.tar.gz

cd tapdata-x.x.x
```

2. 编辑 "application.yml" 文件，输入 access code: xxxxxxx

Access Code 可以通过点击顶部的邮件进入个人中心界面，在这个界面中，您可以获取到专属Access Code。

3. 启动 agent

```
./agent.sh start
```

当您启动Agent后，可以通过点击左侧菜单栏的进程进入进程管理界面，查看Agent运行状态。



## 3. 安装 Enterprise Tapdata

如果您希望试用或者使用我们的 Enterprise Tapdata 请联系我们：**team@tapdata.io**

获取到 Enterprise Tapdata 二进制文件后，转到该目录并执行以下命令：

1. 将安装包解压到指定目录下：

    ```
    tar zxvf tapdata-vx.x.x-xxxxx.tar.gz
    ```

2. 进入软件目录：

    ```
    cd tapdata-vx.x.x
    ```

3. 启动 Tapdata：

    ```
    ./tapdata start
    ```
    

首次安装需要根据提示框输入一些必要信息。

```
Please enter tapdata port. (Default: 3030)
```
网页浏览端口，默认3030

```
Please enter backend url, comma separated list. (Default: http://127.0.0.1:3030)
```
后端地址，默认 http://127.0.0.1:3030

```
Please enter api server port. (Default: 3080)
```
API Server 端口，默认3080

```
Does MongoDB require username/password?((y/n))
```
中间库 mongodb 是否启用认证，若未启用则输入 n，若启用则输入y，若上一步输入 y，则下一步会需要输入中间库 mongodb 的账号名密码

```
Please enter mongodb connection string without username and password (Default: mongodb://127.0.0.1:27017/tapdata)
```
输入中间库的连接字符串，如果是开启认证，连接字符串为：`mongodb://127.0.0.1:27017/tapdata?authSource=admin`

然后，您可以输入默认用户名 `admin@admin.com` 密码：`admin` ）。

完成安装后，您可以打开浏览器并输入

```
http://您的服务器:3030/
```

为了保证您的服务能够正常使用，请确认防火墙开通：

| 服务 | 端口 | 说明 |
| -------- | -------- | ------ |
| 源端 Mysql | 3306(默认) | 对 Tapdata 所在的服务器开通 |
| 源端 Oracle  | 1521(默认) | 对 Tapdata 所在的服务器开通 |
| 源端 Sql Server | 1433(默认) | 对 Tapdata 所在的服务器开通 |
| Tapdata 数据采集器 | 无 | 所在的服务器能够访问到所有源端数据库 |
| Tapdata API Server | 3080(默认) | 允许访问，能够被 Tapdata Portal 访问到 |
| Tapdata Portal | 3030(默认) | 允许访问，能够被 Tapdata API Server 访问到 |
