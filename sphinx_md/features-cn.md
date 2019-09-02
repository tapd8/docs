# 产品特性

## 数据采集

### 具备数据源为数据库的数据采集能力

| 特性 | 描述 |
| -------- | -------- |
| Oracle | 支持的数据库版本有：10g, 11g, 12c |
| MySQL | 支持的数据库版本有：5.5, 5.6, 5.7 |
| SQL Server | 支持的数据库版本有：2008, 2012, 2016 |
| Sybase | 支持的数据库版本有：15.7 ASE |
| MongoDB | 支持的数据库版本有：3.6, 4.0, 4.2 |


### 具备数据源为文件夹的数据采集能力

| 特性 | 描述 |
| -------- | -------- |
| 本地文件夹 | 支持Windows、Linux本地文件夹 |
| 共享目录 | 支持Linux共享目录 |
| FTP | 支持Linux、Windows标准FTP服务 |


### 具备数据源为文件的数据采集能力

| 特性 | 描述 |
| -------- | -------- |
| Excel | 支持单个excel包含一个sheet |
| CSV | 支持自定义分隔符 |
| XML | 支持基本XML格式 |
| Json | 支持数组表达式以及一行一个对象 |

### 具备数据建模能力

- 具备一对一，一对多，多对一的组合关联
- 具备 js 的二次开发能力
- 具备跨库跨表联合查询能力

## 数据发布

- 具备数据修改、查询、删除能力
- 具备 OAuth 认证
- 具备标准 RESTFul API 格式
- 具备自定义数据接口能力
- 具备丰富的数据查询条件组合能力
- 具备自主发布接口测试文档能力
- 具备流量监控管理能力

## 其他

- 具备数据源全量数据采集和增量数据采集能力
- 具备数据质量检核规则建模能力
- 具备数据清洗能力
- 具备重复数据剔除能力

# 产品限制

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
- Oracle 不支持的数据库引擎：
  - Tables using table compression 
- 源库同步到 MongoDB 时，不支持数组中再嵌套一层数组的结构
- 不支持带属性的XML
- 不具备聚合查询能力