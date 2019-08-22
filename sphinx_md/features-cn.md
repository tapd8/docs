# 产品特性

## 数据采集


| 特性 | 描述 | 备注 |
| -------- | -------- | ------ |
| 具备数据源为数据库的数据采集能力 | 支持的数据库种类有：
    - Oracle 10g，Oracle 11g，Oracle 12C
    - MySQL：
    - SQL Server
    - Sybase
    - MongoDB | 暂不支持：
    - 源库DDL操作不支持（新建表、修改表结构、创建索引）
    - Oracle 10g版本不支持增量同步 |
| MySQL：  | string | 必须 |
| SQL Server | string | 必须 |
| Sybase | string | 必须 |
| MongoDB | string | 必须 |


- 具备数据源为数据库的数据采集能力
  - 支持的数据库种类有：
    - Oracle 10g，Oracle 11g，Oracle 12C
    - MySQL：
    - SQL Server
    - Sybase
    - MongoDB
- 具备数据源为文件夹的数据采集能力
- 具备数据源为文件的数据采集能力
- 具备数据源全量数据采集和增量数据采集能力
- 具备转换规则建模能力
- 具备数据质量检核规则建模能力
- 具备分发数据建模能力
- 具备数据清洗能力
- 具备重复数据剔除能力


## 数据发布

- 具备错误数据修改能力

## 数据治理