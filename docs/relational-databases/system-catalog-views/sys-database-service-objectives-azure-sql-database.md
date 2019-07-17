---
title: sys.database_service_objectives （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- 弹性池
- 弹性池管理
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 4174e59fd451d1d709decbbc8955c9fe2329703e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079415"
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>sys.database_service_objectives （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

如果有，将 Azure SQL 数据库或 Azure SQL 数据仓库，返回的版本 （服务层）、 服务目标 （定价层） 和弹性池名称。 如果登录到 Azure SQL 数据库服务器中的 master 数据库，返回所有数据库的信息。 对于 Azure SQL 数据仓库，您必须连接到 master 数据库。  
  
  
 有关定价的信息，请参阅[SQL 数据库选项和性能：SQL 数据库定价](https://azure.microsoft.com/pricing/details/sql-database/)并[SQL 数据仓库定价](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。  
  
 若要更改服务设置，请参阅[ALTER DATABASE （Azure SQL 数据库）](../../t-sql/statements/alter-database-azure-sql-database.md)并[ALTER DATABASE （Azure SQL 数据仓库）](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)。  
  
 Sys.database_service_objectives 视图包含以下各列。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|database_id|INT|在 Azure SQL 数据库服务器的实例中是唯一的数据库的 ID。 使用可加入[sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|版本|sysname|数据库或数据仓库服务层：**基本**，**标准**， **Premium**或**数据仓库**。|  
|service_objective|sysname|数据库的定价层。 如果数据库是在弹性池中，则返回**ElasticPool**。<br /><br /> 上**基本**层，返回**基本**。<br /><br /> **标准服务层中的单个数据库**返回以下值之一：S0、 S1、 S2、 S3、 S4、 S6、 S7、 S9 或 S12。<br /><br /> **高级层中的单个数据库**返回以下值：P1、 P2、 P4、 P6、 P11 或 P15。<br /><br /> **SQL 数据仓库**返回 DW100 通过 DW30000c。|  
|elastic_pool_name|sysname|名称[弹性池](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)属于数据库。 返回**NULL**如果数据库是单一数据库或数据 warehoue。|  
  
## <a name="permissions"></a>权限  
 需要**dbManager**的主数据库上的权限。  在数据库级别，用户必须是创建者或所有者。  
  
## <a name="examples"></a>示例  
 可以运行此示例中，在 master 数据库或 Azure SQL 数据库的用户数据库上。 查询将返回名称、 服务和数据库的性能层信息。  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
