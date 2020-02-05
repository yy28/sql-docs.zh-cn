---
title: ALTER EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 236749303a05b54f37be5e24f10f56fc6f5bc41d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "71227160"
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  修改用于创建外部表的外部数据源。 外部数据源可以是适用于 SQL SERVER 的 Hadoop 和 Azure blob 存储 (WASBS) 或适用于 Azure SQL 数据仓库的 Azure blob 存储 (WASBS) 或 Azure Data Lake Storage (ABFSS/ADL)。 

## <a name="syntax"></a>语法  

```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later) and APS
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ] 

-- Modify an external data source pointing to Azure Blob storage or Azure Data Lake storage
-- Applies to: Azure SQL Data Warehouse
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        [LOCATION = '<location prefix>://<location path>']
        [, CREDENTIAL = credential_name ] 
```

## <a name="arguments"></a>参数  
 data_source_name 指定数据源的用户定义名称。 该名称必须是唯一的。

 LOCATION = 'server_name_or_IP' 提供连接协议和外部数据源的路径。

 RESOURCE_MANAGER_LOCATION = ‘\<IP address;Port>’（不适用于 Azure SQL 数据仓库）指定 Hadoop 资源管理器位置。 如果指定，查询优化器可以选择通过使用 Hadoop 的计算功能预处理 PolyBase 查询的数据。 这是基于开销的决策。 这称为谓词下推，可以显著减少 Hadoop 和 SQL之间传输的数据量，并因此提高查询性能。

 CREDENTIAL = Credential_Name 指定命名凭据。 请参阅 [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

TYPE = [HADOOP | BLOB_STORAGE]   
适用对象：  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。
仅对于大容量操作，`LOCATION` 必须是有效的 Azure Blob 存储 URL。 请勿将 **、文件名或共享访问签名参数放在 / URL 的末尾**`LOCATION`。
必须使用 `SHARED ACCESS SIGNATURE` 作为标识创建所使用的凭据。 有关共享访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。

  

## <a name="remarks"></a>备注
 一次只能修改一个源。 修改同一个源的并发请求会导致一个语句等待。 但是，可以同时修改不同的源。 此语句可以与其他语句同时运行。

## <a name="permissions"></a>权限  
 需要 ALTER ANY EXTERNAL DATA SOURCE 权限。
 > [!IMPORTANT]  
 > ALTER ANY EXTERNAL DATA SOURCE 权限授予任何主体创建和修改任何外部数据源对象的权限，还授予访问数据库上所有数据库作用域凭据的权限。 必须将此权限视为高度特权，因此必须仅授予系统中受信任的主体。


## <a name="examples"></a>示例  
 下面的示例更改了现有数据源的位置和资源管理器位置。

```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```

 下面的示例更改了用于连接到现有数据源的凭据。

```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```

 以下示例将凭证更改为新位置。 此示例是为 Azure SQL 数据仓库创建的外部数据源。 

```  
ALTER EXTERNAL DATA SOURCE AzureStorage_west SET
   LOCATION = 'wasbs://loadingdemodataset@updatedproductioncontainer.blob.core.windows.net',
   CREDENTIAL = AzureStorageCredential
```
