# 介绍

## 1. Tapdata 简介

Tapdata Replicator 是一种混合数据库复制产品。它旨在提供不同类型的数据库之间的实时数据库更改复制。例如，您可以将数据从 Oracle 复制到 MongoDB，或从 MySQL 复制到 Elastic Search 等。此外，Tapdata 还可用于在两个 MongoDB 集群之间复制数据。



## 2. 应用场景

### 2.1 Oracle 到 MongoDB 数据迁移

您正在 MongoDB 上构建应用程序，但您的应用程序所需的数据（例如客户数据或订单数据）当前位于 Oracle 数据库中。出于多种原因，您尚无法停用 Oracle 。因此，您可以使用 Tapdata 以实时方式将数据从 Oracle 复制到 MongoDB 。

这也适用于MSSQL，MySQL等。

### 2.2 MongoDB 到 MongoDB 集群复制

MongoDB 具有强大的内置复制功能，但它运行在复制集中。如果您希望将更改从一个群集复制到另一个群集，或者打算构建"双活"类型的部署，则可以使用 Tapdata 来帮助您实现。



## 3. 支持的数据库类型

### 3.1 支持的源数据库

- Oracle 11g，12c
- MSSQL 2008，2012
- MySQL 5.6，5.7
- Sybase ASE 15,16
- MongoDB 3.2，3.4，3.6，4.0

### 3.2 支持的目标数据库

- MongoDB 3.2，3.4，3.6，4.0
- Elastic Search(To be released)

## 4. 产品特性

### 4.1 数据采集

#### 4.1.1 具备数据源为数据库的数据采集能力

| 特性 | 描述 |
| -------- | -------- |
| Oracle | 支持的数据库版本有：10g, 11g, 12c |
| MySQL | 支持的数据库版本有：5.5, 5.6, 5.7 |
| SQL Server | 支持的数据库版本有：2008, 2012, 2016 |
| Sybase | 支持的数据库版本有：15.7 ASE |
| MongoDB | 支持的数据库版本有：3.6, 4.0, 4.2 |


#### 4.1.2 具备数据源为文件夹的数据采集能力

| 特性 | 描述 |
| -------- | -------- |
| 本地文件夹 | 支持Windows、Linux本地文件夹 |
| 共享目录 | 支持Linux共享目录 |
| FTP | 支持Linux、Windows标准FTP服务 |


#### 4.1.3 具备数据源为文件的数据采集能力

| 特性 | 描述 |
| -------- | -------- |
| Excel | 支持单个excel包含一个sheet |
| CSV | 支持自定义分隔符 |
| XML | 支持基本XML格式 |
| Json | 支持数组表达式以及一行一个对象 |

#### 4.1.4 具备数据建模能力

- 具备一对一，一对多，多对一的组合关联
- 具备 js 的二次开发能力
- 具备跨库跨表联合查询能力

### 4.2 数据发布

- 具备数据修改、查询、删除能力
- 具备 OAuth 认证
- 具备标准 RESTFul API 格式
- 具备自定义数据接口能力
- 具备丰富的数据查询条件组合能力
- 具备自主发布接口测试文档能力
- 具备流量监控管理能力

### 4.3 其他

- 具备数据源全量数据采集和增量数据采集能力
- 具备数据质量检核规则建模能力
- 具备数据清洗能力
- 具备重复数据剔除能力

## 5 产品限制

- 源端关系型数据库 DDL 操作不支持（新建表、修改表结构、创建索引）
- 不支持 Oracle 到 Oracle 的多表合并
- Oracle 不支持的数据种类：
  - Oracle timestamp 精度为微秒，MongoDB 时间精度为毫秒
  - INTERVAL YEAR TO MONTH
  - INTERVAL DAY TO SECOND
  - RAW
  - LONG RAW
  - BFILE
  - Object refs
  - XMLTYPE
  - Collections (nested tables and VARRAYs)
  - Simple and nested abstract datatypes (ADTs)
- Oracle 不支持的表属性：
  - Tables using table compression 
- Oracle 其它限制：
  - 不支持连接到CDB。
  - 空的 BLOB/CLOB 字段会在目标端映射为NULL。
  - 不支持对Primary Key的Update操作。
  - CDC不支持动态视图。
- 源库同步到 MongoDB 时，不支持数组中再嵌套一层数组的结构
- 不支持带属性的XML
- 不具备聚合查询能力
