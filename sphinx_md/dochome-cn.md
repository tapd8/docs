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


