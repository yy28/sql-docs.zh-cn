---
title: "ALTER 外部数据源 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: f74a105226f1ae113287f1c337c1c33e81bb09ae
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="alter-external-data-source-transact-sql"></a>ALTER 外部数据源 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  修改用于创建外部表的外部数据源。 外部数据源可以是 Hadoop 或 Azure blob 存储 (WASB)。  
  
## <a name="syntax"></a>语法  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later), Azure SQL Data Warehouse,
               Parallel Data Warehouse    
ALTER EXTERNAL DATA SOURCE data_source_name SET  
    {   
        LOCATION = 'server_name_or_IP' [,] |  
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |  
        CREDENTIAL = credential_name  
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017), Azure SQL Database,
               Azure SQL Data Warehouse, Parallel Data Warehouse
ALTER EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>参数  
 data_source_name  
 指定数据源的用户定义名称。 该名称必须是唯一的。  
  
 位置 = 'server_name_or_IP  
 指定的服务器或 IP 地址的名称。  
  
 RESOURCE_MANAGER_LOCATION =\<IP 地址;端口 >'  
 指定 Hadoop 资源管理器位置。 如果指定，查询优化器可以选择通过使用 Hadoop 的计算功能预处理 PolyBase 查询的数据。 这是基于开销的决策。 调用谓词下推，这可以显著减少 Hadoop 和 SQL、 之间传输的数据量，并因此提高查询性能。  
  
 凭据 = Credential_Name  
 指定的命名的凭据。 请参阅[CREATE DATABASE SCOPED CREDENTIAL &#40;Transact SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  

类型 = BLOB_STORAGE   
**适用于：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。   
对于大容量操作只，`LOCATION`必须是有效的 Azure Blob 存储的 URL。 不要将放在 **/** 、 文件名称，或共享访问签名参数末尾`LOCATION`URL。   
必须使用创建所使用，凭据`SHARED ACCESS SIGNATURE`作为标识。 有关共享访问签名的详细信息，请参阅[使用共享访问签名 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。

  
  
## <a name="remarks"></a>注释  
 仅单个源可以修改一次。 修改同一源的并发请求会导致一个语句等待。 但是，可以在同一时间修改不同的源。 此外，这此语句可以与并发运行其他语句。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY EXTERNAL DATA SOURCE 权限。  
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 权限授予任何主体能够创建和修改任何外部数据源对象，并因此，它还授予访问数据库上的所有数据库范围凭据的功能。 此权限必须被视为高特权级别，并因此必须被授予到受信任的主体仅在系统中。

  
## <a name="examples"></a>示例  
 下面的示例将更改的位置和资源管理器位置的现有数据源。  
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET  
     LOCATION = 'hdfs://10.10.10.10:8020',  
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'  
    ;  
  
```  
  
 下面的示例将更改要连接到现有的数据源的凭据。  
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET  
   CREDENTIAL = new_hadoop_user  
    ;  
```  
  
  

