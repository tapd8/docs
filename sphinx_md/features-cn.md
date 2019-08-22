# 产品特性

## 数据采集

### 具备数据源为数据库的数据采集能力

| 特性 | 描述 | 备注 |
| -------- | -------- | ------ |
| Oracle | 支持的数据库版本有：10g, 11g, 12c | - 源库DDL操作不支持（新建表、修改表结构、创建索引） <br> - Oracle 10g版本不支持增量同步 <br> - 不支持的数据种类： <br> &nbsp;&nbsp; - INTERVAL YEAR TO MONTH <br> &nbsp;&nbsp; - INTERVAL DAY TO SECOND <br> &nbsp;&nbsp; - RAW <br> &nbsp;&nbsp; - LONG RAW <br> &nbsp;&nbsp; - BFILE <br> &nbsp;&nbsp; - Object refs <br> &nbsp;&nbsp; - XMLTYPE <br> &nbsp;&nbsp; - Collections (nested tables and VARRAYs) <br> &nbsp;&nbsp; - Simple and nested abstract datatypes (ADTs) <br> - 数据库引擎： <br> &nbsp;&nbsp; - Tables using table compression |
| MySQL | 支持的数据库版本有：5.5, 5.6, 5.7 | - 源库DDL操作不支持（新建表、修改表结构、创建索引） |
| SQL Server | 支持的数据库版本有：2008, 2012, 2016 | - 源库DDL操作不支持（新建表、修改表结构、创建索引） |
| Sybase | 支持的数据库版本有：15.7 ASE | - 源库DDL操作不支持（新建表、修改表结构、创建索引） |
| MongoDB | 支持的数据库版本有：3.6, 4.0, 4.2 | 源库同步到MongoDB时，不支持数组中再嵌套一层数组的结构 |


### 具备数据源为文件夹的数据采集能力

| 特性 | 描述 | 备注 |
| -------- | -------- | ------ |
| 本地文件夹 | 支持Windows、Linux本地文件夹 |  |
| 共享目录 | 支持Linux共享目录 | 不支持Windows共享目录 |
| FTP | 支持Linux、Windows标准FTP服务 |  |


### 具备数据源为文件的数据采集能力

| 特性 | 描述 | 备注 |
| -------- | -------- | ------ |
| Excel | 支持单个excel包含一个sheet | 不支持多个sheet，及合并单元格等复杂格式 |
| CSV | 支持自定义分隔符 |  |
| XML | 支持基本XML格式 | 不支持带属性的XML |
| Json | 支持数组表达式以及一行一个对象 |  |

### 具备数据建模能力

- 具备一对一，一对多，多对一的组合关联
- 具备 js 的二次开发能力
- 具备跨库跨表联合查询能力
- 不具备聚合查询能力

### 其他

- 具备数据源全量数据采集和增量数据采集能力
- 具备数据质量检核规则建模能力
- 具备数据清洗能力
- 具备重复数据剔除能力

## 数据发布

- 具备错误数据修改、查询、删除能力
- 具备 OAuth 认证
- 具备标准 RESTFul API 格式
- 具备自定义数据接口能力
- 具备