# 产品特性

## 数据采集

### 具备数据源为数据库的数据采集能力

| 特性 | 描述 | 备注 |
| -------- | -------- | ------ |
| Oracle | 支持的数据库版本有：10g, 11g, 12c | - 源库DDL操作不支持（新建表、修改表结构、创建索引） \n Oracle 10g版本不支持增量同步 \n - 不支持的数据种类： \n   - INTERVAL YEAR TO MONTH \n   - INTERVAL DAY TO SECOND \n   - RAW \n   - LONG RAW \n   - BFILE \n   - Object refs \n   - XMLTYPE \n   - Collections (nested tables and VARRAYs) \n   - Simple and nested abstract datatypes (ADTs) \n - 数据库引擎： \n   - Tables using table compression |
| MySQL | 支持的数据库版本有：5.5, 5.6, 5.7 | - 源库DDL操作不支持（新建表、修改表结构、创建索引） |
| SQL Server | 支持的数据库版本有：2008, 2012, 2016 | - 源库DDL操作不支持（新建表、修改表结构、创建索引） |
| Sybase | 支持的数据库版本有：15.7 ASE | - 源库DDL操作不支持（新建表、修改表结构、创建索引） |
| MongoDB | 支持的数据库版本有：3.6, 4.0, 4.2 | 源库同步到MongoDB时，不支持数组中再嵌套一层数组的结构 |


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