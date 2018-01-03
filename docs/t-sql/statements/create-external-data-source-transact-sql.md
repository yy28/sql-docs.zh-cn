---
title: "创建外部数据源 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs: TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
ms.assetid: 75d8a220-0f4d-4d91-8ba4-9d852b945509
caps.latest.revision: "58"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 283971bbd1bfe04b26860f56601c315ac5244717
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="create-external-data-source-transact-sql"></a>创建外部数据源 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  为 PolyBase、 弹性数据库查询或 Azure Blob 存储创建外部数据源。 根据方案，语法方面明显不同。 为 PolyBase 创建的数据源不能用于弹性数据库查询。  同样，不能针对 PolyBase 等使用的弹性数据库查询创建的数据源。 
  
> [!NOTE]  
>  PolyBase 仅支持 SQL Server 2016、 Azure SQL 数据仓库和并行数据仓库。 仅在 Azure SQL 数据库 v12 上或更高版本支持弹性数据库查询。  
  
 对于 PolyBase 情况下，外部数据源是 Hadoop 文件系统 (HDFS)、 Azure 存储 blob 容器或 Azure 数据湖存储。 有关详细信息，请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 对于弹性数据库查询方案，外部的源是分片映射管理器 （在 Azure SQL 数据库） 或远程数据库 （在 Azure SQL 数据库）。  使用[sp_execute_remote &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md)后创建的外部数据源。 有关详细信息，请参阅[弹性数据库查询](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  

  Azure Blob 存储外部数据源支持`BULK INSERT`和`OPENROWSET`语法中，且不同于 Azure Blob 存储用于 PolyBase。
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- PolyBase only:  Hadoop cluster as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,
        LOCATION = 'hdfs://NameNode_URI[:port]'  
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]  
        [, CREDENTIAL = credential_name ]
    )
[;]  
  
-- PolyBase only: Azure Storage Blob as data source   
-- (on SQL Server 2016 and Azure SQL Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]

-- PolyBase only: Azure Data Lake Store
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net',
    CREDENTIAL = AzureStorageCredential
);

-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, JOB_TRACKER_LOCATION = 'JobTracker_URI[:port]' ]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source 
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP,
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
    )
[;]
  
-- Elastic Database query only: a shard map manager as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = SHARD_MAP_MANAGER,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '\<ElasticDatabase_ShardMapManagerDb'>,  
        CREDENTIAL = <ElasticDBQueryCred>,  
        SHARD_MAP_NAME = '<ShardMapName>'  
    )  
[;]  
  
-- Elastic Database query only: a remote database on Azure SQL Database as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = RDBMS,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '<Remote_Database_Name>',  
        CREDENTIAL = <SQL_Credential>  
    )  
[;]  

-- Bulk operations only: Azure Storage Blob as data source   
-- (on SQL Server 2017 or later, and Azure SQL Database).
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net/container_name'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>参数  
 *data_source_name*指定数据源的用户定义名称。 名称必须是在 SQL Server、 Azure SQL 数据库和 Azure SQL 数据仓库中的数据库中是唯一的。 名称必须是在并行数据仓库中的服务器中是唯一的。
  
 类型 = [HADOOP |于包含 SHARD_MAP_MANAGER |RDBMS |BLOB_STORAGE]  
 指定的数据源类型。 使用 HADOOP，Hadoop 外部数据源时或适用于 Hadoop 的 Azure 存储 blob。 在 Azure SQL 数据库上创建分片的弹性数据库查询的外部数据源时，请使用于包含 SHARD_MAP_MANAGER。 使用 RDBMS 外部数据源的跨数据库查询 Azure SQL 数据库上的弹性数据库查询。  执行大容量操作使用时使用 BLOB_STORAGE[大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md)或[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)与[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。
  
位置 = \<location_path > **HADOOP**    
对于 HADOOP，指定 Hadoop 群集的统一资源标识符 (URI)。  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI： 计算机名称或 IP 地址的 Hadoop 群集 Namenode。  
端口： Namenode IPC 端口。 通过 Hadoop 中的 fs.default.name 配置参数指示这一点。 如果未指定的值，将默认使用 8020。  
例如：`LOCATION = 'hdfs://10.10.10.10:8020'`

有关 Azure blob 存储与 Hadoop 配合使用，指定用于连接到 Azure blob 存储的 URI。  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb [s]: 指定 Azure blob 存储的协议。 [S] 是可选的并指定安全的 SSL 连接;从 SQL Server 发送的数据安全地加密通过 SSL 协议。 我们强烈建议使用 wasbs 而不是 wasb。 请注意，该位置可以使用 asv [s]，而不是 wasb [s]。 Asv [s] 语法已弃用，并在未来版本中将删除。  
容器： 指定 Azure blob 存储容器的名称。 若要指定域的存储帐户的根容器，而不是容器名称中使用的域名。 根容器是只读的因此数据无法重新写入到的容器。  
account_name: Azure 存储帐户的完全限定的域名 (FQDN)。  
例如：`LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

为 Azure 数据湖存储位置指定用于连接到 Azure 数据湖存储区的 URI。



**于包含 SHARD_MAP_MANAGER**   
 有关于包含 SHARD_MAP_MANAGER，指定承载 Azure SQL 数据库或 Azure 虚拟机上的 SQL Server 数据库中的分片映射管理器的逻辑服务器名称。
 
 ```
 CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
  (TYPE = SHARD_MAP_MANAGER,
  LOCATION = '<server_name>.database.windows.net',
  DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
  CREDENTIAL = ElasticDBQueryCred,
  SHARD_MAP_NAME = 'CustomerIDShardMap'
) ;
```

有关分步教程，请参阅[弹性查询的分片 （水平分区） 入门](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)。
  
**RDBMS**   
对于 RDBMS，指定 Azure SQL 数据库中的远程数据库的逻辑服务器名称。  

```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';  
  
CREATE DATABASE SCOPED CREDENTIAL SQL_Credential    
WITH IDENTITY = '<username>',  
SECRET = '<password>';  
  
CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH   
    (TYPE = RDBMS,   
    LOCATION = '<server_name>.database.windows.net',   
    DATABASE_NAME = 'Customers',   
    CREDENTIAL = SQL_Credential   
) ;   
```  
  
RDBMS 的分步教程，请参阅[跨数据库查询 （垂直分区） 入门](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/)。  

**BLOB_STORAGE**   
对于大容量操作只，`LOCATION`必须是有效的 Azure Blob 存储和容器的 URL。 不要将放在 **/** 、 文件名称，或共享访问签名参数末尾`LOCATION`URL。   
必须使用创建所使用，凭据`SHARED ACCESS SIGNATURE`作为标识。 有关共享访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。 有关访问 blob 存储的示例，请参阅示例 F 的[大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md)。 

  
 RESOURCE_MANAGER_LOCATION =*ResourceManager_URI*[:*端口*]  
 指定 Hadoop 资源管理器位置。 如果指定，查询优化器可以基于开销的决策，Hadoop 的计算功能使用 MapReduce 预处理 PolyBase 查询的数据。 调用谓词下推，这可以显著减少 Hadoop 和 SQL、 之间传输的数据量，并因此提高查询性能。  
  
 当未指定时，将计算推送到 Hadoop 使 PolyBase 查询的被禁用。  
 
如果未指定端口，则默认值由 'hadoop connectivity' 配置为使用当前设置。

|Hadoop 连接|默认资源管理器端口|
|-------------------|-----------------------------|
|@shouldalert|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

有关 Hadoop 分发版和版本支持的每个连接值的完整列表，请参阅[PolyBase 连接配置 (Transact SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。
  
> [!IMPORTANT]  
>  RESOURCE_MANAGER_LOCATION 值是一个字符串，并创建外部数据源时不验证。 访问位置时，输入值不正确可能会导致将来的延迟。  
  
 Hadoop 示例：  
  
-   Hortonworks HDP 2.0、 2.1、 2.2。 在 Windows 上的 2.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Hortonworks HDP 1.3 Windows 上：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0、 2.1、 2.2 和 2.3 在 Linux 上：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   在 Linux 上的 Hortonworks HDP 1.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   在 Linux 上的 Cloudera 4.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   在 Linux 上的 Cloudera 5.1 5.11:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 凭据 = *credential_name*  
 指定对外部数据源进行身份验证的数据库范围凭据。 有关示例，请参阅[C.创建 Azure blob 存储外部数据源](../../t-sql/statements/create-external-data-source-transact-sql.md#credential)。 若要创建一个凭据，请参阅[CREATE CREDENTIAL (Transact SQL)](../../t-sql/statements/create-credential-transact-sql.md)。 请注意不允许匿名访问的公共数据集需要凭据。 
  
 DATABASE_NAME = *QueryDatabaseName*  
 （适用于 RDBMS) 充当分片映射管理器 （适用于包含 SHARD_MAP_MANAGER) 的数据库或远程数据库的名称。  
  
 SHARD_MAP_NAME = *ShardMapName*  
 有关于包含 SHARD_MAP_MANAGER 仅。 分片映射的名称。 有关创建分片映射的详细信息，请参阅[弹性数据库查询入门](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>PolyBase 特定说明  
有关支持的外部数据源的完整列表，请参阅[PolyBase 连接配置 (Transact SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。

 若要使用 PolyBase，你需要创建这三个对象：  
  
-   外部数据源。  
  
-   外部文件格式，并  
  
-   外部表引用的外部数据源和外部文件格式。  
  
## <a name="permissions"></a>权限  
 需要在 SQL DW、 SQL Server、 AP 2016 和 SQL DB 数据库拥有 CONTROL 权限。

> [!IMPORTANT]  
>  在以前版本的 PDW 中，创建外部数据源需要 ALTER ANY EXTERNAL DATA SOURCE 权限。
  
  
## <a name="error-handling"></a>错误处理  
 如果外部的 Hadoop 数据源相关 RESOURCE_MANAGER_LOCATION 定义不一致，将发生运行时错误。 也就是说，不能指定引用相同的 Hadoop 群集并提供一个而不是针对其他资源管理器位置的两个外部数据源。  
  
 创建外部数据源对象时，SQL 引擎不验证存在的外部数据源。 如果在查询执行过程，数据源不存在，则将出错。  
  
## <a name="general-remarks"></a>一般备注  
PolyBase，对于外部数据源是数据库范围的 SQL Server 和 SQL 数据仓库中。 该服务器的作用域是并行数据仓库中。
  
对于 PolyBase，RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION 定义时，查询优化器将请考虑优化通过启动地图的每个查询减少外部 Hadoop 源服务器和将计算下推上的作业。 这是完全基于开销的决策。  

若要确保在出现故障时 Hadoop NameNode 的成功 PolyBase 查询，请考虑使用适用于 NameNode Hadoop 群集的虚拟 IP 地址。 有关 Hadoop NameNode 不使用虚拟的 IP 地址，如果发生 Hadoop NameNode 故障转移时必须到 ALTER EXTERNAL DATA SOURCE 对象以指向新位置。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 在相同的 Hadoop 群集位置上定义的所有数据源必须 RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION 都使用相同的设置。 如果没有不一致，将发生运行时错误。  
  
 如果使用名称设置 Hadoop 群集和外部数据源将为群集位置使用的 IP 地址，PolyBase 仍必须能够解析群集名称，使用数据源时。 若要解析的名称，必须启用 DNS 转发器。  
  
## <a name="locking"></a>锁定  
 外部数据源对象上采用共享的锁。  
  
##  <a name="examples"></a>示例： SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. 创建引用 Hadoop 的外部数据源  
若要创建外部数据源引用 Hortonworks 或 Cloudera Hadoop 群集，请指定计算机名称或 Hadoop Namenode 和端口的 IP 地址。  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. 创建使用启用的下推到 Hadoop 引用的外部数据源  
指定 RESOURCE_MANAGER_LOCATION 选项以启用到 Hadoop 使 PolyBase 查询的推计算。 启用后，PolyBase 将使用基于开销的决策来确定是否应会查询计算被推送到 Hadoop 或所有数据都应都移动来处理 SQL Server 中的查询。
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. 创建外部数据源引用 Kerberos 保护的 Hadoop  
若要验证是否 Kerberos 保护的 Hadoop 群集，请检查 Hadoop 的 core-site.xml 中 hadoop.security.authentication 属性的值。 若要引用 Kerberos 保护的 Hadoop 群集，必须指定数据库范围的凭据包含 Kerberos 用户名和密码。 数据库主密钥用于加密数据库范围的凭据密钥。 
  
```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1 
WITH IDENTITY = '<hadoop_user_name>', 
SECRET = '<hadoop_password>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (
    TYPE = HADOOP, 
    LOCATION = 'hdfs://10.10.10.10:8050', 
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050', 
    CREDENTIAL = HadoopUser1
);
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. 创建外部数据源，以引用 Azure blob 存储
若要创建外部数据源引用 Azure blob 存储容器，指定 Azure blob 存储 URI 和数据库范围的凭据，其中包含你的 Azure 存储帐户密钥。

在此示例中，外部数据源是调用 dailylogs 下名为 myaccount 的 Azure 存储帐户的 Azure blob 存储容器。 Azure 存储外部数据源是为仅; 数据传输并不支持谓词下推。

此示例演示如何创建到 Azure 存储空间的身份验证的数据库范围凭据。 中的数据库凭据机密指定 Azure 存储帐户密钥。 指定数据库中的任何字符串作用域凭据标识，它不会向 Azure 存储进行身份验证使用。 然后，在创建外部数据源的语句中使用凭据。

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>示例： Azure SQL 数据库

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. 创建分片映射管理器外部数据源
若要创建外部数据源引用于包含 SHARD_MAP_MANAGER，指定承载 Azure SQL 数据库或 Azure 虚拟机上的 SQL Server 数据库中的分片映射管理器的逻辑服务器名称。

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = SHARD_MAP_MANAGER,
    LOCATION = '<server_name>.database.windows.net',
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
    CREDENTIAL = ElasticDBQueryCred,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
);
```

### <a name="f-create-an-rdbms-external-data-source"></a>F. 创建 RDBMS 外部数据源
若要创建外部数据源引用 RDBMS，请在 Azure SQL 数据库中指定远程数据库的逻辑服务器名称。

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = RDBMS, 
    LOCATION = '<server_name>.database.windows.net', 
    DATABASE_NAME = 'Customers', 
    CREDENTIAL = SQL_Credential 
);
```

## <a name="examples-azure-sql-data-warehouse"></a>示例： Azure SQL 数据仓库

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. 创建引用 Azure 数据湖存储的外部数据源
Azure 数据湖存储连接根据你 ADLS URI 和 Azure 活动目录应用程序的服务主体。 处找不到用于创建此应用程序的文档[数据湖存储身份验证使用 Active Directory](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)。

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = '<ADLS URI>'
)
```



## <a name="examples-parallel-data-warehouse"></a>示例： 并行数据仓库

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. 创建使用启用的下推到 Hadoop 引用的外部数据源
指定 JOB_TRACKER_LOCATION 选项以启用到 Hadoop 使 PolyBase 查询的推计算。 启用后，PolyBase 将使用基于开销的决策来确定是否应会查询计算被推送到 Hadoop 或所有数据都应都移动来处理 SQL Server 中的查询。 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. 创建外部数据源，以引用 Azure blob 存储
若要创建外部数据源，以引用 Azure blob 存储容器，指定 Azure blob 存储 URI 为外部数据源位置。 将你的 Azure 存储帐户密钥添加到 PDW core-site.xml 文件进行身份验证。

在此示例中，外部数据源是调用 dailylogs 下名为 myaccount 的 Azure 存储帐户的 Azure blob 存储容器。 Azure 存储外部数据源为仅数据传输，并且不支持谓词下推。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>示例： 大容量操作   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. 创建从 Azure Blob 存储中检索数据的大容量操作的外部数据源。   
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。   
使用大容量操作中使用以下数据源[大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md)或[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)。 必须使用创建所使用，凭据`SHARED ACCESS SIGNATURE`作为标识。 有关共享访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
若要查看在使用此示例，请参阅[大容量插入](../../t-sql/statements/bulk-insert-transact-sql.md)。
  
## <a name="see-also"></a>另请参阅
[ALTER 外部数据源 (Transact SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)   
[创建外部 TABLE AS SELECT &#40;Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[创建 TABLE AS SELECT &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

