# Tapdata 常见问题

## 作业运行时日志提示：Stopped sync lag maker;

此错误消息表示没有足够的权限来读取Oracle重做日志。请参阅[Oracle配置指南](connection-config-cn.md)页面，在DBA的帮助下正确设置访问权限。


## 运行 job 时出现此错误：java.sql.SQLRecoverableException：No more data to read from socket

尝试一下操作：
  
- 检查 Oracle 的 SQLNET.EXPIRE_TIME 设置，设置更大的值
- 检查系统的 ulimit 设置
- 检查 Oracle 连接池以查看它是否溢出。
- 检查 Oracle 数据库上的连接数

## Tapdata 是否支持视图？

为了提供实时复制功能，Tapdata 需要监视事务日志文件。只有对物理表所做的更改才会生成事务日志。因此，Tapdata 目前不支持视图。

## 如何更改默认用户的登录名（admin@admin.com）？

在 tapdata 安装目录下，运行以下脚本以查看默认用户登录

```shell
etc/update_default_user.sh
```