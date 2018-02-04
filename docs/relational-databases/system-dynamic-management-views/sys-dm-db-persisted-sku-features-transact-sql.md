---
title: "sys.dm_db_persisted_sku_features (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server], feature restrictions
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0af6dc4a6c8031be8a33a44d2c00265d5c58ed0
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbpersistedskufeatures-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  某些功能[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]更改的方式，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将信息存储在数据库文件中。 这些功能仅限于特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 不能将包含这些功能的数据库移到不支持这些功能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 使用 sys.dm_db_persisted_sku_features 动态管理视图列出在当前数据库中启用的特定于版本的功能。
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|在数据库中启用但并非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都支持的功能的外部名称。 必须先删除此功能，然后才能将数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有可用版本。|  
|feature_id|**int**|与功能关联的功能 ID。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]中创建已分区表或索引。|  
  
## <a name="permissions"></a>权限  
 需要对数据库拥有 VIEW DATABASE STATE 权限。  
  
## <a name="remarks"></a>注释  
 如果没有可能会限制由特定版本的功能由数据库，视图会返回任何行。  
  
 sys.dm_db_persisted_sku_features 可能列表限制到特定数据库更改了以下功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本：  
  
-   **ChangeCapture**： 指示数据库已启用变更数据捕获。 若要删除变更数据捕获，使用[sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)存储过程。 有关详细信息，请参阅[关于变更数据捕获 (SQL Server)](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)。  
  
-   **ColumnStoreIndex**： 指示该至少一个表具有列存储索引。 若要使数据库能够将移动到的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支持此功能，请使用[DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)或[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)语句以删除列存储索引。 有关详细信息，请参阅[列存储索引](../../relational-databases/indexes/columnstore-indexes-overview.md)。  
  
    **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。  
  
-   **压缩**： 指示至少一个表或索引使用数据压缩或 vardecimal 存储格式。 若要使数据库能够将移动到的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支持此功能，请使用[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)语句以删除数据压缩。 若要删除 vardecimal 存储格式，请使用 sp_tableoption 语句。 有关详细信息，请参阅 [Data Compression](../../relational-databases/data-compression/data-compression.md)。  
  
-   **MultipleFSContainers**： 指示数据库使用多个 FILESTREAM 容器。 该数据库必须具有多个容器 （文件） 的 FILESTREAM 文件组。 有关详细信息，请参阅 [FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)。  
  
-   **InMemoryOLTP**： 指示数据库使用内存中 OLTP。 数据库具有 MEMORY_OPTIMIZED_DATA 文件组。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
  **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。 
  
-   **分区。** 指示数据库包含已分区表、已分区索引、分区方案或分区函数。 若要使数据库能够移动到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 或 Developer 以外的版本，将表修改到单个分区上是不够的。 必须删除相应的已分区表。 如果该表包含数据，请使用 SWITCH PARTITION 将每个分区转换成无分区表。 然后删除已分区表、分区方案和分区函数。  
  
-   **TransparentDataEncryption.** 指示使用透明数据加密对数据库进行加密。 若要删除透明数据加密，请使用 ALTER DATABASE 语句。 有关详细信息，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。  

> [!NOTE]
> 从开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]Service Pack 1，这些功能都可在多个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本，并不只局限于企业版或开发人员版。

 若要确定数据库是否使用仅限于特定版本的任何功能，请对数据库执行下面的语句：  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [SQL Server 2016 的各版本和支持的功能](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [版本和 SQL Server 2017 支持的功能](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
