---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 986a658c315241e14efd6fd10b170aaf9fb17da0
ms.sourcegitcommit: b2a29f9659f627116d0a92c03529aafc60e1b85a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59516523"
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  为 PolyBase 或弹性数据库查询创建外部数据源。 根据具体方案，语法存在显著差异。 为 PolyBase 创建的外部数据源不能用于弹性数据库查询。  同样，为弹性数据库查询创建的外部数据源不能用于 PolyBase 等。 
  
> [!NOTE]  
>  仅在 SQL Server 2016（或更高版本）、Azure SQL 数据仓库和并行数据仓库上支持 PolyBase。 仅在 Azure SQL 数据库 v12 或更高版本上支持弹性数据库查询。  
  
 对于 PolyBase 方案，外部数据源是 Hadoop 文件系统 (HDFS)、Azure 存储 blob 容器或 Azure Data Lake Store。 有关详细信息，请参阅 [PolyBase 入门](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 对于弹性数据库查询方案，外部源是分片映射管理器（在 Azure SQL 数据库上）或远程数据库（在 Azure SQL 数据库上）。  在创建外部数据源之后可使用 [sp_execute_remote（Azure SQL 数据库）](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md)。 有关详细信息，请参阅[弹性数据库查询](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  

  Azure Blob 存储外部数据源支持 `BULK INSERT` 和 `OPENROWSET` 语法，与用于 PolyBase 的 Azure Blob 存储不同。
    
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
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
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

-- PolyBase only: Azure Data Lake Store Gen 2
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE ABFS 
WITH
(
              TYPE=HADOOP,
              LOCATION='abfs://<container>@<AzureDataLake account_name>.dfs.core.windows.net',
              CREDENTIAL=ABFS_Credemt
);
GO


-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]
        [, CREDENTIAL = credential_name]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source   
-- (on Parallel Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
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
 *data_source_name*   指定数据源的用户定义名称。 该名称必须在 SQL Server 上的数据库、Azure SQL 数据库和 Azure SQL 数据仓库中是唯一的。 该名称必须在并行数据仓库中的服务器上是唯一的。
  
 TYPE = [ HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 指定数据源类型。 当外部数据源是 Hadoop 或适用于 Hadoop 的 Azure 存储 blob 时，可使用 HADOOP。 为弹性数据库查询创建外部数据源以便在 Azure SQL 数据库上进行分片时，可使用 SHARD_MAP_MANAGER。 对于 Azure SQL 数据库上的弹性数据库查询，可将 RDBMS 与跨数据库查询的外部数据源一起使用。  在使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 对 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 执行批量操作时，可使用 BLOB_STORAGE。
  
LOCATION = \<location_path> HADOOP    
对于 HADOOP，指定 Hadoop 群集的统一资源标识符 (URI)。  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI：Hadoop 群集 Namenode 的计算机名称或 IP 地址。  
port：Namenode IPC 端口。 这通过 Hadoop 中的 fs.default.name 配置参数进行指示。 如果未指定该值，则默认情况下使用 8020。  
例如：`LOCATION = 'hdfs://10.10.10.10:8020'`

对于具有 Hadoop 的 Azure blob 存储，指定用于连接到 Azure blob 存储的 URI。  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb[s]：指定 Azure blob 存储的协议。 [s] 是可选的，指定安全 SSL 连接；从 SQL Server 发送的数据会通过 SSL 协议安全地进行加密。 强烈建议使用“wasbs”而不是“wasb”。 请注意，位置可以使用 asv[s] 而不是 wasb[s]。 asv[s] 已弃用，在未来的版本中将删除。  
container：指定 Azure blob 存储容器的名称。 若要指定域的存储帐户的根容器，请使用域名而不是容器名称。 根容器是只读的，因此数据无法重新写入容器中。  
account_name：Azure 存储帐户的完全限定的域名 (FQDN)。  
例如：`LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

对于 Azure Data Lake Store，位置指定用于连接到 Azure Data Lake Store 的 URI。



**SHARD_MAP_MANAGER**   
 对于 SHARD_MAP_MANAGER，指定托管 Azure SQL 数据库中的分片映射管理器或 Azure 虚拟机上的 SQL Server 数据库的 SQL 数据库服务器名称。
 
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

有关分步教程，请参阅[跨扩展云数据库进行报告（预览）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)。
  
**RDBMS**   
对于 RDBMS，指定 Azure SQL 数据库中远程数据库的 SQL 数据库服务器名称。  

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
  
有关 RDBMS 的分步教程，请参阅[跨数据库查询（纵向分区）入门（预览）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/)。  

**BLOB_STORAGE**   
此类型仅用于批量操作，对于 Azure Blob 存储和容器，`LOCATION` 必须是有效的 URL。 请勿将 /、文件名或共享访问签名参数放在 `LOCATION` URL 的末尾。 如果 Blob 对象不是公共的，则需要 `CREDENTIAL`。 例如： 
```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH (  TYPE = BLOB_STORAGE, 
        LOCATION = 'https://****************.blob.core.windows.net/invoices', 
        CREDENTIAL= MyAzureBlobStorageCredential    --> CREDENTIAL is not required if a blob has public access!
);
```
所用的凭据必须使用 `SHARED ACCESS SIGNATURE` 作为标识进行创建、不应在 SAS 令牌中具有前导 `?`、必须对应加载的文件（例如 `srt=o&sp=r`）至少具有读取权限，并且有效期应有效（所有日期均采用 UTC 时间）。 例如：
```sql
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential 
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';
```

有关共享访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。 有关访问 blob 存储的示例，请参阅 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 的示例 F。 
>[!NOTE] 
>若要从 Azure Blob 存储加载到 SQL DW 或并行数据仓库，Secret 必须是 Azure 存储密钥。

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*port*]'  
 指定 Hadoop 资源管理器位置。 指定时，查询优化器可以通过将 Hadoop 的计算功能与 MapReduce 一起使用，来进行基于成本的决策以便 PolyBase 查询预处理数据。 这称为谓词下推，可以显著减少 Hadoop 和 SQL之间传输的数据量，并因此提高查询性能。  
  
 未指定此选项时，会为 PolyBase 查询禁用将计算推送到 Hadoop。  
 
如果未指定端口，则默认值使用“hadoop 连接”配置的当前设置进行确定。

|Hadoop 连接|默认资源管理器端口|
|-------------------|-----------------------------|
|1|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

有关每个连接值支持的 Hadoop 分发版和版本的完整列表，请参阅 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。
  
> [!IMPORTANT]  
>  RESOURCE_MANAGER_LOCATION 值是字符串，在创建外部数据源时不进行验证。 输入错误值可能会导致将来在访问位置时出现延迟。  
  
 Hadoop 示例：  
  
-   Windows 上的 Hortonworks HDP 2.0、2.1、2.2、 2.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Windows 上的 Hortonworks HDP 1.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Linux 上的 Hortonworks HDP 2.0、2.1、2.2、2.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Linux 上的 Hortonworks HDP 1.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Linux 上的 Cloudera 4.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Linux 上的 Cloudera 5.1 - 5.11：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENTIAL = credential_name  
 指定用于对外部数据源进行身份验证的数据库范围凭据。 有关示例，请参阅 [C. 创建 Azure blob 存储外部数据源](../../t-sql/statements/create-external-data-source-transact-sql.md#credential)。 若要创建凭据，请参阅 [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md)。 请注意，允许进行匿名访问的公共数据集不需要 CREDENTIAL。 
  
 DATABASE_NAME = 'QueryDatabaseName'  
 充当分片映射管理器（对于 SHARD_MAP_MANAGER）或远程数据库（对于 RDBMS）的数据库的名称。  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 仅用于 SHARD_MAP_MANAGER。 分片映射的名称。 有关创建分片映射的详细信息，请参阅[跨扩展云数据库进行报告（预览）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>特定于 PolyBase 的说明  
有关受支持的外部数据源的完整列表，请参阅 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。

 若要使用 PolyBase，需要创建以下三个对象：  
  
-   外部数据源。  
  
-   外部文件格式，以及  
  
-   引用外部数据源和外部文件格式的外部表。  
  
## <a name="permissions"></a>权限  
 需要 SQL DW、SQL Server、APS 2016 和 SQL DB 中的数据库上的 CONTROL 权限。

> [!IMPORTANT]  
>  在以前版本的 PDW 中，创建外部数据源需要 ALTER ANY EXTERNAL DATA SOURCE 权限。
  
  
## <a name="error-handling"></a>错误处理  
 如果外部 Hadoop 数据源在定义 RESOURCE_MANAGER_LOCATION 方面不一致，则会发生运行时错误。 也就是说，无法指定引用相同 Hadoop 群集的两个外部数据源，然后为其中一个提供资源管理器位置，而不为另一个提供。  
  
 创建外部数据源对象时，SQL 引擎不验证外部数据源是否存在。 如果数据源在查询执行过程中不存在，则会发生错误。  
  
## <a name="general-remarks"></a>一般备注  
对于 PolyBase，外部数据源在 SQL Server 和 SQL 数据仓库中适用于数据库范围。 它并行数据仓库中适用于服务器范围。
  
对于 PolyBase，定义 RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION 时，查询优化器会考虑通过在外部 Hadoop 源上启动 map reduce 作业并下推计算，来优化每个查询。 这完全是基于开销的决策。  

若要确保 PolyBase 查询在 Hadoop NameNode 发生故障转移时成功进行，请考虑对 Hadoop 群集的 NameNode 使用虚拟 IP 地址。 如果不对 Hadoop NameNode 使用虚拟 IP 地址，则发生 Hadoop NameNode 故障转移时，必须 ALTER EXTERNAL DATA SOURCE 对象以指向新位置。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 在相同 Hadoop 群集位置上定义的所有数据源都必须对 RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION 使用相同设置。 如果存在不一致，则会发生运行时错误。  
  
 如果使用名称设置 Hadoop 群集，而外部数据源对群集位置使用 IP 地址，则 PolyBase 仍必须能够在使用数据源时解析群集名称。 若要解析名称，必须启用 DNS 转发器。  
 
暂不支持类型为 `hadoop` 的 SAS 令牌，仅支持将它用于存储帐户访问密钥。 尝试创建类型为 `hadoop` 的外部数据源和使用 SAS 凭据可能会失败，并看到以下错误：

`Msg 105019, Level 16, State 1 - EXTERNAL TABLE access failed due to internal error: 'Java exception raised on call to HdfsBridge_Connect. Java exception message: Parameters provided to connect to the Azure storage account are not valid.: Error [Parameters provided to connect to the Azure storage account are not valid.] occurred while accessing external file.'`
  
## <a name="locking"></a>锁定  
 在 EXTERNAL DATA SOURCE 对象上采用共享锁。  
  
##  <a name="examples"></a>示例：SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. 创建外部数据源以引用 Hadoop  
若要创建外部数据源以引用 Hortonworks 或 Cloudera Hadoop 群集，请指定 Hadoop Namenode 的计算机名称或 IP 地址以及端口。  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. 创建外部数据源以引用 Hadoop 并启用下推  
指定 RESOURCE_MANAGER_LOCATION 选项以便为 PolyBase 查询启用到 Hadoop 的下推计算。 启用后，PolyBase 会使用基于开销的决策来确定是应将查询计算推送到 Hadoop 还是应移动所有数据以在 SQL Server 中处理查询。
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. 创建外部数据源以引用受 Kerberos 保护的 Hadoop  
若要验证 Hadoop 群集是否受 Kerberos 保护，请检查 Hadoop core-site.xml 中的 hadoop.security.authentication 属性值。 若要引用受 Kerberos 保护的 Hadoop 群集，必须指定包含 Kerberos 用户名和密码的数据库范围凭据。 数据库主密钥用于加密数据库范围凭据密钥。 
  
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

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. 创建外部数据源以引用 Azure blob 存储
若要创建外部数据源以引用 Azure blob 存储容器，请指定 Azure blob 存储 URI 以及包含 Azure 存储帐户密钥的数据库范围凭据。

在此示例中，外部数据源是名为 myaccount 的 Azure 存储帐户下的 Azure blob 存储容器（名为 dailylogs）。 Azure 存储外部数据源是仅用于数据传输；不支持谓词下推。

此示例演示如何创建数据库范围凭据以用于对 Azure 存储进行身份验证。 在数据库凭据机密中指定 Azure 存储帐户密钥。 在数据库范围凭据标识中指定任何字符串，它不会用于对 Azure 存储进行身份验证。 随后会在创建外部数据源的语句中使用凭据。

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = BLOB_STORAGE, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>示例：Azure SQL Database

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. 创建分片映射管理器外部数据源
若要创建外部数据源以引用 SHARD_MAP_MANAGER，请指定托管 Azure SQL 数据库中的分片映射管理器或 Azure 虚拟机上的 SQL Server 数据库的 SQL 数据库服务器名称。

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
若要创建外部数据源以引用 RDBMS，请指定 Azure SQL 数据库中的远程数据库的 SQL 数据库服务器名称。

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

## <a name="examples-azure-sql-data-warehouse"></a>示例：Azure SQL 数据仓库

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. 创建外部数据源以引用 Azure Data Lake Store
Azure Data Lake Store 连接基于 ADLS URI 和 Azure Active Directory 应用程序的服务主体。 可以在[使用 Azure Active Directory 进行 Data Lake Store 服务到服务身份验证](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)中找到有关创建此应用程序的文档。

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



## <a name="examples-parallel-data-warehouse"></a>示例：并行数据仓库

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. 创建外部数据源以引用 Hadoop 并启用下推
指定 JOB_TRACKER_LOCATION 选项以便为 PolyBase 查询启用到 Hadoop 的下推计算。 启用后，PolyBase 会使用基于开销的决策来确定是应将查询计算推送到 Hadoop 还是应移动所有数据以在 SQL Server 中处理查询。 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. 创建外部数据源以引用 Azure blob 存储
若要创建外部数据源以引用 Azure blob 存储容器，请指定 Azure blob 存储 URI 作为外部数据源位置。 将 Azure 存储帐户密钥添加到 PDW core-site.xml 文件以用于身份验证。

在此示例中，外部数据源是名为 myaccount 的 Azure 存储帐户下的 Azure blob 存储容器（名为 dailylogs）。 Azure 存储外部数据源是仅用于数据传输，不支持谓词下推。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>示例：批量操作   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. 创建外部数据源以用于从 Azure Blob 存储检索数据的批量操作。   
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。   
对使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 的批量操作使用以下数据源。 所用的凭据必须使用 `SHARED ACCESS SIGNATURE` 作为标识进行创建、不应在 SAS 令牌中具有前导 `?`、必须对应加载的文件（例如 `srt=o&sp=r`）至少具有读取权限，并且有效期应有效（所有日期均采用 UTC 时间）。 有关共享访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。   
```sql
CREATE DATABASE SCOPED CREDENTIAL AccessAzureInvoices 
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '(REMOVE ? FROM THE BEGINNING)******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
若要查看这一使用中的示例，请参阅 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md#f-importing-data-from-a-file-in-azure-blob-storage)。
  
## <a name="see-also"></a>另请参阅
[ALTER EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[CREATE TABLE AS SELECT（Azure SQL 数据仓库）](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

