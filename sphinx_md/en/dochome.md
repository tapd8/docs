# Introduction

## 1. Tapdata Introduction

Tapdata Replicator is a hybrid database replication product. It is designed to provide real time database change replication between different type of databases. For example, you can replicate data from Oracle to MongoDB, or from MySQL to Elastic Search etc.  In addition Tapdata can also be used to replicate data between two MongoDB clusters. 



## 2. Application Scenario

### 2.1 Oracle to MongoDB data migraiton

You are building apps on MongoDB, but the data your app needs, such as customer data or order data, are currently in Oracle database. For a number of reasons, you cannot decommission your Oracle just yet. So you use Tapdata to replicate the data from Oracle to MongoDB, in real time fashion. 

This also applies to MSSQL, MySQL etc. 

### 2.2 MongoDB to MongoDB intra-cluster replication

MongoDB has great built-in replication feature, but it works within a replicaset. If you wish to replicate changes from one cluster to another, or intend to build a dual-active type of deployment, you may use Tapdata to help you to achieve the goal. 



## 3. Supported Database Types

### 3.1 Supported source databases

- Oracle 11g, 12c
- MSSQL 2008, 2012
- MySQL 5.6, 5.7 
- Sybase ASE 15, 16
- MongoDB 3.2, 3.4, 3.6, 4.0

### 3.2 Supported Target databases

- MongoDB 3.2, 3.4, 3.6, 4.0
- Elastic Search(To be released)


