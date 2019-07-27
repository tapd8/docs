# 数据发布

## 1. 概述

Tap data 数据发布是将 MongoDB 中的 Collection 通过简单的配置创建 REST API 接口，开放给开发者或支持 REST API 数据源的其他应用系统使用；默认提供了增、删、查、改等基本API，用户可以添加自定义查询API。



## 2. 安装

数据发布产品依赖Java1.8+、MongoDB 4+、NodeJS10+ 运行环境。运行数据发布产品，默认使用3030和3080端口，可根据实际情况调整默认配置。

安装包内以内置 node，并在安装过程中会帮您完成环境初始化。所以您不用额外安装 node。

下面使用到的地址都是默认本地部署：
- 管理端地址：http://127.0.0.1:3030
- API Server地址：http://127.0.0.1:3080

完整的安装过程可以参考[安装说明](installation-cn.md)

1. 将安装包解压到指定目录下：

    ```
    tar zxvf tapdata-vx.x.x-xxxxx.tar.gz
    ```

2. 进入软件目录：

    ```
    cd tapdata-vx.x.x
    ```

3. 启动 API Server：

    ```
    ./tapdata start apiserver
    ```
    
首次安装需要根据提示框输入一些必要信息。

![](../images/apiserver-cn-1.png)

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
输入中间库的连接字符串，如果是开启认证，连接字符串为：`mongodb://<account>:<password>@127.0.0.1:27017/tapdata?authSource=admin`



## 3. 注册客户端应用

开发者设计开发的应用程序或者其他需要调用 API 接口的应用程序（统称客户端应用）在接入数据发布系统前需要先在注册，注册完成后，得到一个专属客户端ID（client_id）和客户端密钥（client_secret）。

注：客户端密钥是客户端应用取得 API 访问授权的重要依据，应妥善保存，避免公共网络环境传输。

### 3.1 创建客户端应用
使用管理员账号登录 Tap data，打开【数据发布】->【API 客户端】->【创建】：

![](../images/apiserver-cn-2.png)​​

![](../images/apiserver-cn-3.png)

说明：
- Client Name: 客户端名称
- Grant Types: 允许客户端应用使用的授权类型
    - Implicit: 隐式授权方式，认证过程需要用户输入用户名密码确认授权，适合网页应用请求API 接口获取数据。
    - Client credentials: 客户端密钥授权方式，客户端使用密钥直接换取访问令牌，不需要用户授权确认，适合后台应用直接调用API接口。
- Client Secret: 客户端密钥，使用 client credentials 认证授权方式时，必须填写。
- Scopes: 允许客户端应用访问的接口范围。直接决定这个客户端可以使用的 API 接口。
- Redirect URIs: 当使用 implicit 授权方式时，用于回调客户端应用并传递访问 API 接口的令牌等参数。

### 3.2 设置客户端应用访问权限

API 权限是基于 Tap data 角色实现控制；管理员可以在【数据发布】->【API 客户端】->【编辑】页面的 Scopes 字段选择允许客户端应用访问的 API 接口。

​​![](../images/apiserver-cn-4.png)​​



## 4. 发布API

### 4.1 发布API

创建发布 API 无需关心数据模型，系统自动跟据 MongoDB 中的数据识别加载数据模型。

#### 4.1.1 创建数据源

使用管理员账号登录 Tap data，打开【数据源】->【新建连接】：

![](../images/apiserver-cn-5.png)​​

说明：
- Database Type: 数据库类型，目前数据发布只支持MongoDB
- Connection Name: 连接名称
- Connection Type: 数据发布使用，请固定选择 Target
- Database URI: MongoDB URI

注：测试连接失败时请检查连接参数配置是否有误；只有测试连接通过后，才可以正常发布API。

#### 4.1.2 创建API

使用管理员账号登录 Tap data，打开【数据发布】->【API 发布】->【创建】：

![](../images/apiserver-cn-6.png)​​

​​![](../images/apiserver-cn-7.png)​​

说明：
- Connection: 数据源，指定要发布的 API 使用的数据源
- Collection: 数据集，指定要发布的 API 是那个数据集
- Version API: 版本，可以未发布的 API 指定一个版本，这个版本将影响到接口请求地址
- BasePath API: 接口的基础路径
- Path API: 接口的访问路径，客户端应用实际访问接口地址为：http://api_server_host:port/api/${version}/${basePath}

#### 4.1.3 发布API

使用管理员账号登录 Tap data，打开【数据发布】->【API 发布】：

![](../images/apiserver-cn-8.png)​​

说明：
点击要发布 API 上面的蓝色【纸飞机】图标及完成发布操作；再次点击这个图标取消发布API

注：点击发布 API 后需要等待10秒左右，后台自动更新 API 接口（右上角API Server状态变化：Running -> Updating -> Running）

#### 4.1.4 变更数据模型，重新发布API

MongoDB 中的 Collection 增加了新的字段时，需要重新加载数据模型，操作如下：
1. 重新测试保存连接：打开【数据源】->【连接】->【编辑】->【测试 & 保存】
2. 重新保存已发布的API：打开【数据发布】->【API 列表】->【编辑】->【保存】

注：上述两步缺一不可；单独重新发布API也无效。

### 4.2 预览发布数据

API 发布完成后，可以在【数据发布】->【数据浏览】页面查看API发布的数据。

![](../images/apiserver-cn-9.png)​​

### 4.3 设置 API 权限

API 权限控制是基于 Tap data 角色实现。管理员可以为每一个API（增、删、查、改）单独设置权限。

打开【数据发布】->【API 发布】->【编辑】->【​​钥匙按钮】：

![](../images/apiserver-cn-10.png)​​



## 5. 自主接入

开发者可以自己编写 API 客户端实现，也可以下载 SDK 直接使用。自主对接流程如下：

![](../images/apiserver-cn-11.png)​​

### 5.1 获取 API 接口访问令牌

API 认证服务是基于 OAuth2.0 实现，默认支持 client credentials、implicit 授权方式，客户端可以按需选择合适的授权方式获取授权

#### 5.1.1 获取 API 访问令牌(client credentials)

- 请求地址

    ```
    POST http://127.0.0.1:3030/oauth/token
    ```

- 请求参数

| 名称 | 类型 | 是否必填 | 说明 |
| -------- | -------- | ------ | ------ |
| grant_type | string | 必须 | 固定值：client_credentials |
| client_id  | string | 必须 | 注册客户端时拿到的客户端ID |
| client_secret | string | 必须 | 注册客户端时拿到的客户端密钥 |

- 响应参数

| 名称 | 类型 | 是否必填 | 说明 |
| :-------- | :-------- | :------ | :------ |
| access_token | string | 必须 | 访问 API Server 的令牌 |
| expires_in  | string | 必须 | 过期时间 |
| refresh_token | string | 可选 |  |
| token_type | string | 可选 | API Server 令牌认证方式，默认为Bearer |

#### 5.1.2 携带访问令牌调用API

客户端每次调用发布的接口都需要提供 access_token 完成鉴权认证。发送请求时，可以将 access_token 放在请求头、请求体或URL参数中；也可以使用 Bearer 方式将 access_token 添加认证请求头信息中，无论使用那种方式，API Server 都会自动获取并完成权限验证。

- ApiKey 方式

    在 request header、request body、request url 中添加 access_token 参数：

    ```
    access_token: eyJhbGciOiJIUzI1NiJ9.eyJjbGllbnRJZCI6ImI1ZmQwMWM1OTk2YTYzNDMyMGViZjUzY2JhYjVmYWRmIiwidXNlcl9pZCI6IjVjZTBiYzUxMzNmZDI5NGI2YTI1YTYzYyIsImNyZWF0ZWRBdCI6MTU1ODM2ODg4NDk0NCwicm9sZXMiOlsiNWNlMGJjNTEzM2ZkMjk0YjZhMjVhNjNjIl0sImV4cGlyZWRhdGUiOjE1NTgzNzA2ODQ5NDR9.fKSCRs2pCNdYYVCYjM-W1OfmQO057EKKOTO1n89Q998
    ```

- Bearer 方式

    在request header 中添加认证参数：

    ```
    Authorization: bearer eyJhbGciOiJIUzI1NiJ9.eyJjbGllbnRJZCI6ImI1ZmQwMWM1OTk2YTYzNDMyMGViZjUzY2JhYjVmYWRmIiwidXNlcl9pZCI6IjVjZTBiYzUxMzNmZDI5NGI2YTI1YTYzYyIsImNyZWF0ZWRBdCI6MTU1ODM2ODg4NDk0NCwicm9sZXMiOlsiNWNlMGJjNTEzM2ZkMjk0YjZhMjVhNjNjIl0sImV4cGlyZWRhdGUiOjE1NTgzNzA2ODQ5NDR9.fKSCRs2pCNdYYVCYjM-W1OfmQO057EKKOTO1n89Q998
    ```

### 5.2 新增记录

- 请求地址

    ```
    POST http://127.0.0.1:3080/api/v1/Logs
    ```

- 请求参数（Content-Type: application/json）

    ```
    {
        "date": "2019-07-18T02:10:45.551Z",  
        "level": "INFO",  
        "loggerName": "com.tapdata.connector.JDBCConnector",  
        "message": "connect to data source successful.",  
        "threadId": 9127,  
        "threadName": "Thread-103"
    }
    ```

- 响应参数（Content-Type: application/json）

    ```
    {
        "_id": "5d2fd6b98749d020d73903ed",  
        "date": "2019-07-18T02:10:45.551Z",  
        "level": "INFO",  
        "loggerName": "com.tapdata.connector.JDBCConnector",  
        "message": "connect to data source successful.",  
        "threadId": 9127,  
        "threadName": "Thread-103"
    }
    ```

### 5.3 根据ID更新记录

- 请求地址

    ```
    PATCH http://127.0.0.1:3080/api/v1/Logs/5d2fd6b98749d020d73903ed
    ```

- 请求参数（Content-Type: application/json）

    ```
    {
        "_id": "5d2fd6b98749d020d73903ed",  
        "date": "2019-07-18T02:10:45.551Z",  
        "level": "ERROR",  
        "loggerName": "com.tapdata.connector.JDBCConnector",  
        "message": "connect to data source fail.",  
        "threadId": 9127,  
        "threadName": "Thread-103"
    }
    ```

- 响应

    响应状态码 204，更新成功。

### 5.4 根据ID删除记录

- 请求地址

    ```
    DELETE http://127.0.0.1:3080/api/v1/Logs/5d2fd6b98749d020d73903ed
    ```

- 响应

    响应状态码 204，删除成功。

### 5.5 根据ID查询记录

- 请求地址

    ```
    GET http://127.0.0.1:3080/api/v1/Logs/5d2fd6b98749d020d73903ed
    ```

- 响应参数（Content-Type: application/json）

    响应码: 200

    ```
    {
        "_id": "5d2fd6b98749d020d73903ed",  
        "date": "2019-07-18T02:10:45.551Z",  
        "level": "ERROR",  
        "loggerName": "com.tapdata.connector.JDBCConnector",  
        "message": "connect to data source fail.",  
        "threadId": 9127,  
        "threadName": "Thread-103"
    }
    ```

### 5.6 分页查询

- 请求地址

    ```
    GET http://127.0.0.1:3080/api/v1/Logs
    ```

- 请求参数（URL Query string）

| 参数名 | 参数值 |
| ----- | ----- |
| filter[skip] | 0 |
| filter[limit] | 10 |
| filter[where][loggerName] | com.tapdata.connector.JDBCConnector |

更多查询条件用法参见【查询条件说明】

- 响应参数（Content-Type: application/json）

    ```
    {
        "data": [    
            {      
                "_id": "5d2fd6b98749d020d73903ed",      
                "date": "2019-07-18T02:10:45.551Z",      
                "level": "ERROR",      
                "loggerName": "com.tapdata.connector.JDBCConnector",      
                "message": "connect to data source fail.",      
                "threadId": 9127,      
                "threadName": "Thread-103"    
            }  
        ],  
        "total": {    
            "count": 1  
        }
    }
    ```

### 5.7 常见响应状态码说明

| 响应状态码 | 说明 |
| --------- | --- |
| 200 | findById、findPage、create、自定义方法 请求处理成功返回。|
| 204 | updateById、deleteById 请求处理成功返回。| 
| 500 | 服务器内部处理错误返回。常见错误：新增记录违反唯一约束、MongoDB Validate 验证失败等。|
| 401 | 认证失败返回。访问令牌过期或未提供访问令牌。|
| 404 | 操作数据不存在返回。根据删除、更新、查询不存在的记录等。|

## 6. 查询条件说明

调用分页查询接口，可以在 URL 查询字符串中添加 “filter” 查询条件过滤数据。

默认支持以下几种过滤器：
- **字段过滤器(Field filter)**: 按需返回指定的字段
- **限定返回记录数过滤器(limit filter)**: 限定返回记录行数
- **跳过指定记录数过滤器(Skip filter)**: 跳过指定行数返回
- **查询条件过滤器(Where filter)**: 根据一组具有逻辑关系的条件查询匹配数据并返回，类似SQL 的 WHERE 子句。

### 6.1 字段过滤器(Field filter)

字段过滤器是指定返回的数据中包含或不包含某些字段。

```
filter[fields][propertyName]=<true|false>&filter[fields][propertyName]=<true|false>...
```

默认情况下，查询返回结果中包含数据模型的所有属性。如果您指定了至少一个字段过滤器的值为 true，那么查询返回结果中将仅包含您专门指定包含的那些字段。

**例子**

只返回 Logs 数据模型中的 level、date、message 字段属性的值：

```
?filter[fields][level]=true&filter[fields][message]=true&filter[fields][date]=true
```

返回的结果：

```
{	
    "data": [      
    {          
        "level": "INFO",          
        "message": "generator controller /home/lg/workspace/nodejs/apig/src/controllers/logs-v-1.controller.ts",         "date": "2019-07-13T09:12:05.134Z"      
    }, {          
        "level": "INFO",          
        "message": "generator controller /home/lg/workspace/nodejs/apig/src/controllers/logs-v-1.controller.ts",         "date": "2019-07-13T09:12:05.134Z"      
    },      ...    
    ]
}
```

### 6.2 限定返回记录数过滤器(limit filter)

限制返回记录总条数等于或小于一个指定的数值。通常与 skip filter 配合使用，实现分页查询。

```
filter[limit]=n
```

**例子**

只返回10条查询结果：

```
?filter[limit]=10
```

### 6.3 跳过指定记录数过滤器(skip filter)

返回第 1 个开始跳过指定个数记录后的查询结果。通常与 limit filter 配合使用，实现分页查询。

```
filter[skip]=n
```

**例子**

查询结果中，从第 10 条记录开始返回：

```
?filter[skip]=10
```

**分页查询例子：**

每页数据显示 10 条记录，查询第 5 页的数据：

```
?filter[limit]=10&filter[skip]=50
```

### 6.4 查询条件过滤器(where filter)

在实现业务逻辑过程中，通常需要使用至少一组具有逻辑关系的查询条件来过滤出需要的数据。

在这里您也可以指定一组或多组查询条件来查询数据。

where filter 通常有两种写法，在下面的第一种写法，表示 指定属性 等于 指定值，即 等值查询；第二种写法表示 指定属性 操作符号 指定值，适用于类似 大于、小于 等逻辑查询。

```
?filter[where][property]=value

?filter[where][property][operator]=value
```

- property: 数据模型中的属性名称
- operator: 逻辑操作符，必须是下面表格中一个

#### 6.4.1 操作符列表

| 操作符号 | 说明 |
| ------- | --- |
| and | 逻辑 AND 操作。|
| or | 逻辑 OR 操作。 |
| gt, gte | 数字大小比较 大于(>)、大于等于(>=)。 |
| lt, lte | 数字大小比较 小于（<）、小于等于（<）。 | 
| between | 区间查询，大于等于第一个值，小于等于第二个值。 | 
| inq, nin | IN / NOT IN 一组值. | 
| like, nlike | LIKE / NOT LIKE 模糊查询 |
| regexp | 正则表达式匹配查询 |

#### 6.4.2 AND / OR 组合条件查询

使用 and / or 操作符号，可以组合两个或多个查询条件调用接口查询数据。

```
filter[where][<and|or>][0]condition1&filter[where][<and|or>][1]condition2...
```

例一，查询 api-server 程序的 INFO 日志：

```
?filter[where][and][0][level]=INFO&filter[where][and][1][loggerName]=api-server
```

例二，查询 api-server 程序的 INFO 日志和 tapdata-managent 程序的 ERROR 日志：

```
?filter[where][or][0][and][0][level]=ERROR&filter[where][or][0][and][1][loggerName]=tapdata-managent&filter[where][or][1][and][0][level]=INFO&filter[where][or][1][and][1][loggerName]=api-server
```

#### 6.4.3 gt / gte / lt / lte / like / nlike / regexp 操作符

```
filter[where][property][operator]=value
```

例一，查询日志时间大于指定日期的日志：

```
?filter[where][date][gte]=2019-07-18T10:26:00.000Z
```

注：日期格式为

例二，正则表达式匹配 message ：

```
?filter[where][message][regexp]=LogsController.*findPage
```

#### 6.4.4 inq / nin 操作符号

```
filter[where][property][<inq | nin>][0]=value1&filter[where][property][<inq | nin>][1]=value2...
```

#### 6.4.5 between 操作符号

```
filter[where][property][<inq | nin>][0]=value1&filter[where][property][<inq | nin>][1]=value2...
```

例一，查询日期在 2019-07-01 到 2019-07-02 之间的日志

```
?filter[where][date][between][0]=2019-07-01T00:00:00.000Z&filter[where][date][between][1]=2019-07-02T00:00:00.000Z
```