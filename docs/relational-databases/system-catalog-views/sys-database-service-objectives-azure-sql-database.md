---
title: sys.database_service_objectives （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 08/30/2016
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- 弹性池
- 弹性池管理
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d222a06a64d53ab26d19206f846edadf69e613ba
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>sys.database_service_objectives （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

返回的版本 （服务层）、 （定价层） 的服务目标和弹性池名称，如果有，Azure SQL 数据库或 Azure SQL 数据仓库。 如果登录到 Azure SQL 数据库服务器中 master 数据库，返回所有数据库上的信息。 为 Azure SQL 数据仓库，你必须连接到 master 数据库。  
  
  
 有关定价的信息，请参阅[SQL 数据库选项和性能： SQL 数据库定价](https://azure.microsoft.com/en-us/pricing/details/sql-database/)和[SQL 数据仓库定价](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。  
  
 若要更改的服务设置，请参阅[ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)和[ALTER DATABASE （Azure SQL 数据仓库）](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)。  
  
 Sys.database_service_objectives 视图包含以下各列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|int|在 Azure SQL 数据库服务器的实例中是唯一的数据库 ID。 与加入[sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|版本|sysname|数据库或数据仓库的服务层：**基本**，**标准**，**高级**，**一般用途**， **业务关键型**，或**数据仓库**。|  
|service_objective|sysname|数据库的定价层。 如果数据库是在弹性池中，则返回**ElasticPool**。<br /><br /> 上**基本**层，返回**基本**。<br /><br /> 标准服务层中的单个数据库返回此层的当前有效值。<br /><br /> 高级层中的单个数据库返回此服务层的当前有效值。<br /><br />一般用途的服务层中的单个数据库返回此服务层的当前有效值。<br /><br />关键业务服务层中的单个数据库返回此服务层的当前有效值。<br /><br /> SQL 数据仓库 SQL 数据仓库中返回当前有效的值。|  
|elastic_pool_name|sysname|名称[弹性池](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)的所属的数据库。 返回**NULL**如果数据库位于单一数据库或数据 warehoue。|  
  
## <a name="permissions"></a>权限  
 需要**dbManager**的主数据库上的权限。  在数据库级别中，用户必须创建者或所有者。  
  
## <a name="examples"></a>示例  
 此示例的主数据库上或在用户数据库上运行。 查询返回名称、 服务和数据库的性能层信息。  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
